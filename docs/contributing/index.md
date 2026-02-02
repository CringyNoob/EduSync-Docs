# Contributing

Thank you for your interest in contributing to EduSync!

## How to Contribute

### 1. Fork & Clone

```bash
git clone https://github.com/YOUR_USERNAME/EduSync.git
cd EduSync
```

### 2. Create a Branch

```bash
git checkout -b feature/your-feature-name
```

### 3. Make Changes & Submit PR

Follow the coding standards and submit a pull request with a clear description.

## Code Style

- Use ES6+ JavaScript
- Follow ESLint configuration
- Use meaningful variable and function names
- Add comments for complex logic

## Commit Message Format

```
feat: add user profile endpoint
fix: resolve login issue
docs: update API documentation
refactor: improve error handling
```

## Development Setup

1. Install dependencies in each service:
   ```bash
   npm install
   ```

2. Set up environment variables (copy `.env.example` to `.env`)

3. Start services:
   ```powershell
   .\start-all-services.ps1
   ```

---

**Thank you for contributing!** 🎉
