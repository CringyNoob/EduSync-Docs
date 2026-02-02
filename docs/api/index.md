# API Reference

Complete API documentation for all EduSync microservices.

## Services Overview

| Service | Port | Base Path | Database |
|:--------|:----:|:----------|:---------|
| [Auth Service](auth-service.md) | `3001` | `/api/auth` | `auth_db` |
| [Marketplace Service](marketplace-service.md) | `3002` | `/api/market` | `market_db` |
| [RentHub Service](renthub-service.md) | `3003` | `/api/renthub` | `rent_db` |
| [NewsBox Service](newsbox-service.md) | `3004` | `/api/newsbox` | `newsbox_db` |
| [Chat Service](chat-service.md) | `3006` | `/api/chat` | `chat_db` |
| [Issue Service](issue-service.md) | `3007` | `/api/issues` | `issue_db` |
| [Notices Service](notices-service.md) | `3005` | `/api/notices` | *In-memory* |

## Authentication

All protected endpoints require a JWT token in the `Authorization` header:

```http
Authorization: Bearer <your-jwt-token>
```

!!! info "Token Storage"
    The frontend stores JWT tokens in `localStorage` under the key `edusync_token`.

## Common Response Formats

=== "Success Response"

    ```json
    {
        "success": true,
        "data": { ... },
        "message": "Operation successful"
    }
    ```

=== "Error Response"

    ```json
    {
        "success": false,
        "error": "Error message",
        "details": { ... }
    }
    ```

=== "Paginated Response"

    ```json
    {
        "success": true,
        "data": [...],
        "pagination": {
            "page": 1,
            "limit": 20,
            "total": 150,
            "pages": 8
        }
    }
    ```

## API Gateway Routes

All requests go through the Gateway at `http://localhost:8000`:

```
/api/auth/*    → localhost:3001/*
/api/market/*  → localhost:3002/*
/api/renthub/* → localhost:3003/*
/api/newsbox/* → localhost:3004/*
/api/notices/* → localhost:3005/notices/*
/api/chat/*    → localhost:3006/*
/api/issues/*  → localhost:3007/*
```

## Quick Links

<div class="grid cards" markdown>

-   :material-lock:{ .lg .middle } __Auth Service__

    ---

    User registration, login, OTP, profiles, role management

    [:octicons-arrow-right-24: View Docs](auth-service.md)

-   :material-store:{ .lg .middle } __Marketplace__

    ---

    Vendors, products, pre-owned, orders, payments

    [:octicons-arrow-right-24: View Docs](marketplace-service.md)

-   :material-key:{ .lg .middle } __RentHub__

    ---

    Rental listings, transactions, availability

    [:octicons-arrow-right-24: View Docs](renthub-service.md)

-   :material-newspaper:{ .lg .middle } __NewsBox__

    ---

    Posts, comments, voting, categories

    [:octicons-arrow-right-24: View Docs](newsbox-service.md)

-   :material-message:{ .lg .middle } __Chat__

    ---

    Conversations, messages, Socket.io events

    [:octicons-arrow-right-24: View Docs](chat-service.md)

-   :material-alert:{ .lg .middle } __Issues__

    ---

    Issue reports, voting, admin management

    [:octicons-arrow-right-24: View Docs](issue-service.md)

</div>
