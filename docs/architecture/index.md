# Architecture

This section covers the system design and architectural decisions behind EduSync.

<div class="grid cards" markdown>

-   :material-sitemap:{ .lg .middle } __System Overview__

    ---

    High-level architecture, data flow, and component interactions.

    [:octicons-arrow-right-24: Overview](overview.md)

-   :material-docker:{ .lg .middle } __Microservices__

    ---

    Deep dive into each backend service, their responsibilities and APIs.

    [:octicons-arrow-right-24: Services](services.md)

</div>

## Architecture Principles

!!! abstract "Design Philosophy"
    
    EduSync follows these core architectural principles:

    - **Microservices** - Each feature domain is a separate service
    - **Single Responsibility** - Services own their data and logic
    - **API Gateway Pattern** - Centralized entry point for all requests
    - **JWT-based Auth** - Stateless authentication across services
    - **Event-driven** - Real-time updates via Socket.io

## Quick Stats

| Metric | Count |
|--------|-------|
| Backend Services | 7 |
| PostgreSQL Databases | 6 |
| API Gateway Routes | 7 |
| Frontend Routes | 30+ |
| React Contexts | 4 |
