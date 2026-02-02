# Frontend

Documentation for the EduSync React frontend application.

## Tech Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| React | 19.2.0 | UI Framework |
| Vite | 7.2.4 | Build Tool |
| React Router | 7.10.1 | Client-side Routing |
| TailwindCSS | 3.4.17 | Utility-first Styling |
| Socket.io Client | 4.7.2 | Real-time Communication |
| Axios | 1.9.0 | HTTP Client |

## Project Structure

```
client/
├── src/
│   ├── components/     # Reusable UI components
│   │   ├── common/     # Shared components (Navbar, Footer)
│   │   ├── Auth/       # Authentication components
│   │   ├── Marketplace/ # Marketplace components
│   │   ├── RentHub/    # Rental components
│   │   └── Chat/       # Chat components
│   ├── pages/          # Page components (routes)
│   ├── context/        # React Context providers
│   ├── services/       # API client modules
│   ├── hooks/          # Custom React hooks
│   └── utils/          # Utility functions
├── public/             # Static assets
│   └── logo.png        # EduSync logo
└── index.html          # Entry HTML file
```

## State Management

EduSync uses **React Context** for global state management:

| Context | Purpose |
|---------|---------|
| `AuthContext` | User authentication, JWT tokens |
| `CartContext` | Shopping cart (localStorage persistence) |
| `ThemeContext` | Light/dark mode toggle |
| `NotificationContext` | Toast notifications |

## Key Features

### Authentication
- JWT token stored in `localStorage` as `edusync_token`
- Auto-refresh on app load
- Protected routes with redirect

### API Communication
- All requests go through Gateway at `http://localhost:8000`
- Axios interceptors add Bearer token automatically
- Error handling with user-friendly notifications

### Real-time Chat
- Socket.io connection to Chat service
- Message persistence and delivery status
- Typing indicators

## Development

```bash
cd client
npm install
npm run dev
```

The frontend runs at `http://localhost:5173` and proxies API requests to the Gateway.
