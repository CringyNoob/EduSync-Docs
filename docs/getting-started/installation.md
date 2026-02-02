# Installation Guide

Complete setup instructions for running EduSync locally.

---

## Prerequisites

Before you begin, ensure you have the following installed:

| Requirement | Version | Purpose |
|-------------|---------|---------|
| **Node.js** | 18.x or higher | Runtime for all services |
| **npm** | 9.x or higher | Package management |
| **Git** | Latest | Version control |
| **PostgreSQL Client** | 14+ | Database management (optional) |

!!! tip "Recommended Tools"
    - **VS Code** with ESLint and Prettier extensions
    - **Thunder Client** or **Postman** for API testing
    - **pgAdmin** or **DBeaver** for database management

---

## Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/CringyNoob/EduSync.git
cd EduSync
```

### 2. Install Dependencies

Install dependencies for all services:

```powershell
# Root dependencies (optional, for shared tools)
npm install

# Auth Service
cd auth-service
npm install
cd ..

# Marketplace Service
cd marketplace-service
npm install
cd ..

# RentHub Service
cd renthub-service
npm install
cd ..

# NewsBox Service
cd newsbox-service
npm install
cd ..

# Notices Service
cd notices-service
npm install
cd ..

# Chat Service
cd chat-service
npm install
cd ..

# Issue Service
cd issue-service
npm install
cd ..

# Gateway
cd gateway
npm install
cd ..

# Frontend Client
cd client
npm install
cd ..
```

!!! tip "PowerShell Script"
    Use the setup script to install all at once:
    ```powershell
    .\setup-all-services.ps1
    ```

### 3. Configure Environment Variables

Each service requires a `.env` file. Create them based on the templates:

=== "auth-service/.env"

    ```env
    PORT=3001
    DB_HOST=pg-1ea37722-aranov1107-6aeb.c.aivencloud.com
    DB_PORT=16231
    DB_USER=your_username
    DB_PASSWORD=your_password
    DB_NAME=auth_db
    DB_SSL=true
    JWT_SECRET=your_jwt_secret
    OTP_SECRET=your_otp_secret
    EMAIL_SERVICE=gmail
    EMAIL_USER=your_email@gmail.com
    EMAIL_PASSWORD=your_app_password
    ```

=== "marketplace-service/.env"

    ```env
    PORT=3002
    DB_HOST=pg-1ea37722-aranov1107-6aeb.c.aivencloud.com
    DB_PORT=16231
    DB_USER=your_username
    DB_PASSWORD=your_password
    DB_NAME=market_db
    DB_SSL=true
    JWT_SECRET=your_jwt_secret
    SSLCOMMERZ_STORE_ID=your_store_id
    SSLCOMMERZ_STORE_PASSWORD=your_store_password
    SSLCOMMERZ_IS_SANDBOX=true
    ```

=== "renthub-service/.env"

    ```env
    PORT=3003
    DB_HOST=pg-1ea37722-aranov1107-6aeb.c.aivencloud.com
    DB_PORT=16231
    DB_USER=your_username
    DB_PASSWORD=your_password
    DB_NAME=rent_db
    DB_SSL=true
    JWT_SECRET=your_jwt_secret
    ```

=== "newsbox-service/.env"

    ```env
    PORT=3004
    DB_HOST=pg-1ea37722-aranov1107-6aeb.c.aivencloud.com
    DB_PORT=16231
    DB_USER=your_username
    DB_PASSWORD=your_password
    DB_NAME=newsbox_db
    DB_SSL=true
    JWT_SECRET=your_jwt_secret
    ```

=== "chat-service/.env"

    ```env
    PORT=3006
    DB_HOST=pg-1ea37722-aranov1107-6aeb.c.aivencloud.com
    DB_PORT=16231
    DB_USER=your_username
    DB_PASSWORD=your_password
    DB_NAME=chat_db
    DB_SSL=true
    JWT_SECRET=your_jwt_secret
    ```

=== "issue-service/.env"

    ```env
    PORT=3007
    DB_HOST=pg-1ea37722-aranov1107-6aeb.c.aivencloud.com
    DB_PORT=16231
    DB_USER=your_username
    DB_PASSWORD=your_password
    DB_NAME=issue_db
    DB_SSL=true
    JWT_SECRET=your_jwt_secret
    ```

!!! warning "Important"
    - The `JWT_SECRET` must be **identical** across all services
    - Use the same database credentials for all services (Aiven PostgreSQL)
    - The Notices Service (3005) doesn't require database configuration

### 4. Start All Services

Use the provided PowerShell script:

```powershell
.\start-all-services.ps1
```

This opens separate terminal windows for each service:

| Service | Port | Terminal Title |
|---------|------|----------------|
| Auth Service | 3001 | 🔐 AUTH SERVICE |
| Marketplace Service | 3002 | 🛒 MARKETPLACE SERVICE |
| RentHub Service | 3003 | 🏠 RENTHUB SERVICE |
| NewsBox Service | 3004 | 📰 NEWSBOX SERVICE |
| Notices Service | 3005 | 📋 NOTICES SERVICE |
| Chat Service | 3006 | 💬 CHAT SERVICE |
| Issue Service | 3007 | 🚨 ISSUE SERVICE |
| API Gateway | 8000 | 🌐 API GATEWAY |
| React Client | 5173 | ⚛️ REACT CLIENT |

### 5. Verify Installation

Open your browser and check:

- **Frontend**: [http://localhost:5173](http://localhost:5173)
- **Gateway**: [http://localhost:8000](http://localhost:8000)
- **Auth Health**: [http://localhost:3001/health](http://localhost:3001/health)

---

## Manual Start (Alternative)

If you prefer starting services manually:

```powershell
# Terminal 1 - Auth Service
cd auth-service
npm start

# Terminal 2 - Marketplace Service
cd marketplace-service
npm start

# Terminal 3 - RentHub Service
cd renthub-service
npm start

# Terminal 4 - NewsBox Service
cd newsbox-service
npm start

# Terminal 5 - Notices Service
cd notices-service
npm start

# Terminal 6 - Chat Service
cd chat-service
npm start

# Terminal 7 - Issue Service
cd issue-service
npm start

# Terminal 8 - Gateway
cd gateway
node server.js

# Terminal 9 - Frontend
cd client
npm run dev
```

---

## Database Setup

### Create Databases

If you're setting up your own PostgreSQL:

```sql
-- Create databases
CREATE DATABASE auth_db;
CREATE DATABASE market_db;
CREATE DATABASE rent_db;
CREATE DATABASE newsbox_db;
CREATE DATABASE chat_db;
CREATE DATABASE issue_db;
```

### Run Schema Scripts

```bash
# Auth database
psql -d auth_db -f auth-service/database-schema.sql

# Market database
psql -d market_db -f marketplace-service/database-schema.sql

# Rent database
psql -d rent_db -f renthub-service/database-schema.sql

# NewsBox database
psql -d newsbox_db -f newsbox-service/database-schema.sql

# Chat database
psql -d chat_db -f chat-service/database-schema.sql

# Issue database
psql -d issue_db -f issue-service/database-schema.sql
```

### Populate Sample Data

```bash
# Must be in this order due to foreign key references
psql -d auth_db -f auth-service/populate-auth-data.sql
psql -d market_db -f marketplace-service/populate-marketplace-data.sql
psql -d rent_db -f renthub-service/populate-renthub-data.sql
```

---

## Stopping Services

```powershell
.\stop-all-services.ps1
```

Or manually kill ports:

```powershell
npx kill-port 3001 3002 3003 3004 3005 3006 3007 8000 5173
```

---

## Troubleshooting

### Port Already in Use

```powershell
# Kill specific port
npx kill-port 3001

# Kill all service ports
npx kill-port 3001 3002 3003 3004 3005 3006 3007 8000 5173
```

### Database Connection Failed

1. Verify `.env` credentials
2. Check if Aiven PostgreSQL is accessible
3. Ensure SSL is enabled (`DB_SSL=true`)

### CORS Errors

1. Ensure Gateway is running
2. Check frontend is using correct API URL
3. Verify CORS origin in gateway configuration

### Service Not Starting

1. Check for missing dependencies: `npm install`
2. Verify `.env` file exists
3. Check logs for specific errors

---

## Next Steps

- [Quick Start Guide](quick-start.md) - Start using EduSync
- [Architecture Overview](../architecture/index.md) - Understand the system
- [API Documentation](../api/index.md) - Explore the APIs
