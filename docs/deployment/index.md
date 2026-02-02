# Deployment

Guides for deploying EduSync to various environments.

## Local Development

See the [Installation Guide](../getting-started/installation.md) for local setup.

## Production Deployment

!!! warning "Coming Soon"
    Detailed production deployment guides are under development.

### Recommended Stack

| Component | Recommended Platform |
|-----------|---------------------|
| Frontend | Vercel, Netlify, Cloudflare Pages |
| Backend Services | Railway, Render, DigitalOcean |
| Database | Aiven PostgreSQL (already configured) |
| Domain & CDN | Cloudflare |

### Environment Variables

Each service requires its own `.env` file. Key variables:

```bash
# Database
DATABASE_URL=postgresql://user:pass@host:port/dbname?sslmode=require

# Authentication
JWT_SECRET=your_jwt_secret_key

# Email (Auth Service)
EMAIL_SERVICE=gmail
EMAIL_USER=your_email
EMAIL_PASSWORD=your_app_password

# Payment (Marketplace)
SSLCOMMERZ_STORE_ID=your_store_id
SSLCOMMERZ_STORE_PASSWORD=your_store_password
```

### Docker Deployment

A `docker-compose.yml` is provided in the project root for containerized deployment:

```bash
docker-compose up -d
```

## Service Ports

Ensure these ports are available/exposed:

| Service | Port |
|---------|------|
| Auth | 3001 |
| Marketplace | 3002 |
| RentHub | 3003 |
| NewsBox | 3004 |
| Notices | 3005 |
| Chat | 3006 |
| Issue | 3007 |
| Gateway | 8000 |
| Frontend | 5173 (dev) |
