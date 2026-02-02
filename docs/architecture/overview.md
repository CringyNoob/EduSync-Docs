# Architecture Overview

EduSync follows a microservices architecture with a React frontend communicating through an API Gateway.

---

## High-Level Architecture

```mermaid
flowchart TB
    subgraph Client Layer
        WEB[React SPA<br/>:5173]
    end
    
    subgraph Gateway Layer
        GW[API Gateway<br/>:8000]
    end
    
    subgraph Service Layer
        AUTH[Auth Service<br/>:3001]
        MARKET[Marketplace<br/>:3002]
        RENT[RentHub<br/>:3003]
        NEWS[NewsBox<br/>:3004]
        NOTICE[Notices<br/>:3005]
        CHAT[Chat Service<br/>:3006]
        ISSUE[Issue Service<br/>:3007]
    end
    
    subgraph Data Layer
        AUTH_DB[(auth_db)]
        MARKET_DB[(market_db)]
        RENT_DB[(rent_db)]
        NEWS_DB[(newsbox_db)]
        CHAT_DB[(chat_db)]
        ISSUE_DB[(issue_db)]
        CACHE[Memory Cache]
    end
    
    WEB --> GW
    GW --> AUTH
    GW --> MARKET
    GW --> RENT
    GW --> NEWS
    GW --> NOTICE
    GW --> CHAT
    GW --> ISSUE
    
    AUTH --> AUTH_DB
    MARKET --> MARKET_DB
    RENT --> RENT_DB
    NEWS --> NEWS_DB
    NOTICE --> CACHE
    CHAT --> CHAT_DB
    ISSUE --> ISSUE_DB
```

---

## Design Principles

### 1. Service Independence
Each microservice is:

- **Self-contained**: Has its own database
- **Independently deployable**: Can be updated without affecting others
- **Single responsibility**: Handles one domain

### 2. API Gateway Pattern
All client requests pass through the gateway:

- **Unified entry point**: Single URL for all APIs
- **Path rewriting**: Simplifies client-side routing
- **CORS handling**: Centralized cross-origin configuration

### 3. Stateless Authentication
JWT-based authentication:

- **Token-based**: No server-side sessions
- **Distributed**: Any service can validate tokens
- **Self-contained**: User info embedded in token

---

## Technology Stack

### Frontend
| Technology | Version | Purpose |
|------------|---------|---------|
| React | 19.2.0 | UI Framework |
| Vite | 7.2.4 | Build Tool |
| React Router | 7.10.1 | Client-side Routing |
| TailwindCSS | 3.4.17 | Styling |
| Socket.io Client | 4.7.2 | Real-time Communication |
| Axios | 1.9.0 | HTTP Client |

### Backend
| Technology | Version | Purpose |
|------------|---------|---------|
| Node.js | 18+ | Runtime |
| Express.js | 4.x | Web Framework |
| PostgreSQL | 14+ | Database |
| Socket.io | 4.7.2 | WebSocket Server |
| JWT | - | Authentication |
| bcrypt | - | Password Hashing |

### Infrastructure
| Component | Technology |
|-----------|------------|
| Database Hosting | Aiven Cloud PostgreSQL |
| Payment Gateway | SSLCommerz (Sandbox) |
| Email Service | Nodemailer (Gmail) |

---

## Request Flow

### Typical API Request

```mermaid
sequenceDiagram
    participant C as Client
    participant G as Gateway :8000
    participant S as Service
    participant D as Database

    C->>G: GET /api/market/vendors
    G->>G: Log request
    G->>G: Strip /api/market prefix
    G->>S: GET /vendors
    S->>D: SELECT * FROM vendors
    D-->>S: Results
    S-->>G: JSON Response
    G-->>C: JSON Response
```

### Authenticated Request

```mermaid
sequenceDiagram
    participant C as Client
    participant G as Gateway
    participant S as Service
    participant A as Auth Middleware

    C->>G: GET /api/renthub/listings/my
    Note over C: Header: Authorization: Bearer <token>
    G->>S: Forward with headers
    S->>A: Validate JWT
    A-->>S: User payload
    S->>S: Fetch user's listings
    S-->>G: JSON Response
    G-->>C: JSON Response
```

---

## Data Flow

### Cross-Service Communication

Services are **stateless** and don't communicate directly. Data correlation happens through:

1. **User IDs**: UUID references across databases
2. **Frontend Orchestration**: Client fetches from multiple services
3. **Gateway Routing**: Single entry point for all requests

```mermaid
flowchart LR
    subgraph auth_db
        U[users]
    end
    
    subgraph market_db
        V[vendors]
        P[products]
    end
    
    subgraph rent_db
        L[listings]
    end
    
    U -.->|owner_id| V
    U -.->|seller_id| P
    U -.->|owner_id| L
    
    style U fill:#e1f5fe
    style V fill:#fff3e0
    style P fill:#fff3e0
    style L fill:#e8f5e9
```

---

## Security Architecture

### Authentication Flow

```mermaid
sequenceDiagram
    participant U as User
    participant F as Frontend
    participant A as Auth Service
    participant E as Email Service

    U->>F: Register with email
    F->>A: POST /auth/register
    A->>E: Send OTP email
    A-->>F: Return temp token
    U->>F: Enter OTP
    F->>A: POST /auth/verify-otp
    A-->>F: Return JWT token
    F->>F: Store in localStorage
```

### JWT Token Structure

```json
{
    "id": "user-uuid",
    "email": "student@uiu.edu",
    "name": "John Doe",
    "roles": ["STUDENT", "VENDOR"],
    "activeRole": "STUDENT",
    "department": "CSE",
    "batch": "52",
    "iat": 1705312800,
    "exp": 1705917600
}
```

---

## Deployment Architecture

### Development

```
┌─────────────────────────────────────────────────────────┐
│                    Developer Machine                     │
├─────────────────────────────────────────────────────────┤
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐    │
│  │ Service │  │ Service │  │ Service │  │ Gateway │    │
│  │  :3001  │  │  :3002  │  │  :3003  │  │  :8000  │    │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘    │
│                        ...                               │
│  ┌─────────────────────────────────────────────────────┐│
│  │              Frontend (Vite) :5173                  ││
│  └─────────────────────────────────────────────────────┘│
└─────────────────────────────────────────────────────────┘
                           │
                           ▼
          ┌────────────────────────────┐
          │   Aiven Cloud PostgreSQL   │
          │   (6 databases)            │
          └────────────────────────────┘
```

### Production (Recommended)

```
                    ┌──────────────┐
                    │   Vercel /   │
                    │   Netlify    │
                    │  (Frontend)  │
                    └──────┬───────┘
                           │
                    ┌──────▼───────┐
                    │  API Gateway │
                    │   (Railway)  │
                    └──────┬───────┘
                           │
    ┌──────────────────────┼──────────────────────┐
    │                      │                      │
┌───▼───┐  ┌───▼───┐  ┌───▼───┐  ┌───▼───┐  ...
│ Auth  │  │Market │  │ Rent  │  │ Chat  │
│Service│  │Service│  │Service│  │Service│
└───┬───┘  └───┬───┘  └───┬───┘  └───┬───┘
    │          │          │          │
    └──────────┴──────────┴──────────┘
                    │
          ┌────────▼────────┐
          │ Aiven PostgreSQL│
          └─────────────────┘
```

---

## Scalability Considerations

### Current Limitations

- **Single instances**: Each service runs as one instance
- **Shared database**: All services use same Aiven cluster
- **Base64 images**: Images stored in database (no CDN)

### Future Improvements

- **Containerization**: Docker for each service
- **Load balancing**: Multiple service instances
- **Object storage**: S3/Cloudinary for images
- **Message queue**: RabbitMQ for async operations
