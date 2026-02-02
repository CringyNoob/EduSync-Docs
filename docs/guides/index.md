# Guides

In-depth guides for using and extending EduSync.

## User Roles

| Role | Capabilities |
|------|-------------|
| **Student** | Browse marketplace, buy products, rent items, chat, report issues |
| **Vendor** | Sell products, manage inventory, process orders |
| **Admin** | Full system access, user management, content moderation |

## Quick Links

- [Installation Guide](../getting-started/installation.md)
- [Quick Start](../getting-started/quick-start.md)
- [API Documentation](../api/index.md)
- [Database Schema](../database/schema.md)

## Troubleshooting

### Common Issues

#### Port Already in Use

```powershell
npx kill-port 3001 3002 3003 3004 3005 3006 3007 8000 5173
```

Or use the provided script:

```powershell
.\stop-all-services.ps1
```

#### Database Connection Failed

1. Verify `.env` credentials are correct
2. Check SSL mode is set to `require`
3. Ensure Aiven database is accessible from your network
4. Try connecting with psql to verify credentials

#### CORS Errors

1. Ensure Gateway is running on port 8000
2. Check that frontend is making requests to `/api/` prefix
3. Verify CORS configuration in `gateway/server.js`

#### Authentication Issues

1. Check if JWT token exists in `localStorage` (key: `edusync_token`)
2. Verify token hasn't expired (7-day expiry)
3. Ensure `Authorization: Bearer <token>` header is set

### Service Health Checks

Verify services are running:

| Service | Health Check URL |
|---------|-----------------|
| Auth | `http://localhost:3001/health` |
| Marketplace | `http://localhost:3002/` |
| RentHub | `http://localhost:3003/health` |
| NewsBox | `http://localhost:3004/health` |
| Notices | `http://localhost:3005/notices` |
| Chat | `http://localhost:3006/health` |
| Issue | `http://localhost:3007/health` |
| Gateway | `http://localhost:8000/` |
