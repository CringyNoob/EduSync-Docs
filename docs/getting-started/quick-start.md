# Quick Start Guide

Get EduSync up and running in under 5 minutes.

---

## TL;DR

```powershell
git clone https://github.com/CringyNoob/EduSync.git
cd EduSync
.\setup-all-services.ps1
# Configure .env files (see below)
.\start-all-services.ps1
# Open http://localhost:5173
```

---

## Step 1: Start All Services

After cloning and installing dependencies, run:

```powershell
.\start-all-services.ps1
```

Wait for all terminals to show "running" messages.

---

## Step 2: Access the Application

Open your browser to [http://localhost:5173](http://localhost:5173)

---

## Step 3: Register an Account

1. Click **Register** in the navigation
2. Fill in your details:
   - Email must be `@uiu.edu` domain
   - Student ID in format `011XXXXXX`
   - Select your department and batch
3. Verify your email with the OTP sent
4. You're in! 🎉

---

## Step 4: Explore Features

### 📰 NewsBox
- Browse campus news and announcements
- Post your own updates (requires approval)
- Upvote/downvote and comment

### 🛒 Marketplace
- Browse vendor shops and food stalls
- View preowned items from students
- Add items to cart and checkout

### 🏠 RentHub
- Find items to rent from other students
- List your own items for rent
- Manage rental transactions

### 💬 Chat
- Join your batch chatroom
- Start direct conversations
- Real-time messaging

### 🚨 Issues
- Report campus issues
- Track issue resolution
- Get updates on your reports

---

## Default Test Accounts

If using populated test data:

| Email | Password | Role |
|-------|----------|------|
| john.smith@uiu.edu | password123 | Student/Vendor |
| sarah.johnson@uiu.edu | password123 | Student |
| admin@uiu.edu | admin123 | Admin |

!!! warning "Development Only"
    These accounts are for testing. Never use in production.

---

## Service Status Check

Verify all services are running:

| Service | URL | Expected |
|---------|-----|----------|
| Gateway | [localhost:8000](http://localhost:8000) | "Gateway is Running" |
| Auth | [localhost:3001/health](http://localhost:3001/health) | Health status |
| Marketplace | [localhost:3002](http://localhost:3002) | Service info |
| RentHub | [localhost:3003/health](http://localhost:3003/health) | Health status |

---

## Next Steps

- 📖 Read the [Installation Guide](installation.md) for detailed setup
- 🏗️ Understand the [Architecture](../architecture/index.md)
- 🔌 Explore the [API Documentation](../api/index.md)
- 🤝 Learn how to [Contribute](../contributing/index.md)
