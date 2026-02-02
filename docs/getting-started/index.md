# Getting Started

Welcome to EduSync! This section will help you set up the project on your local machine.

<div class="grid cards" markdown>

-   :material-download:{ .lg .middle } __Installation__

    ---

    Prerequisites and step-by-step installation guide for all services.

    [:octicons-arrow-right-24: Installation Guide](installation.md)

-   :material-rocket-launch:{ .lg .middle } __Quick Start__

    ---

    Get up and running in under 5 minutes with our quick start guide.

    [:octicons-arrow-right-24: Quick Start](quick-start.md)

</div>

## System Requirements

| Requirement | Minimum | Recommended |
|-------------|---------|-------------|
| **Node.js** | v18.0.0 | v20+ LTS |
| **npm** | v9.0.0 | v10+ |
| **RAM** | 4 GB | 8 GB+ |
| **Disk Space** | 2 GB | 5 GB+ |
| **OS** | Windows 10/macOS/Linux | Windows 11/macOS 14+ |

## Project Structure Overview

```
EduSync/
├── 🔐 auth-service/        # Port 3001 - Authentication
├── 🛒 marketplace-service/ # Port 3002 - Marketplace
├── 🏠 renthub-service/     # Port 3003 - Rentals
├── 📰 newsbox-service/     # Port 3004 - Community Feed
├── 📋 notices-service/     # Port 3005 - UIU Notices
├── 💬 chat-service/        # Port 3006 - Real-time Chat
├── 🚨 issue-service/       # Port 3007 - Issue Reporting
├── 🌐 gateway/             # Port 8000 - API Gateway
├── ⚛️ client/              # Port 5173 - React Frontend
└── 📄 Various config files
```
