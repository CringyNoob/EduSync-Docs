# Database

Database documentation for EduSync's PostgreSQL databases hosted on Aiven Cloud.

<div class="grid cards" markdown>

-   :material-table:{ .lg .middle } __Schema Reference__

    ---

    Complete schema documentation for all six databases.

    [:octicons-arrow-right-24: View Schema](schema.md)

</div>

## Database Overview

EduSync uses **six PostgreSQL databases** hosted on Aiven Cloud:

| Database | Service | Port | Purpose |
|----------|---------|------|---------|
| `auth_db` | Auth Service | 3001 | Users, profiles, OTPs |
| `market_db` | Marketplace Service | 3002 | Vendors, products, orders, payments |
| `rent_db` | RentHub Service | 3003 | Rental listings, transactions |
| `newsbox_db` | NewsBox Service | 3004 | Posts, comments, votes |
| `chat_db` | Chat Service | 3006 | Chatrooms, messages, participants |
| `issue_db` | Issue Service | 3007 | Issue reports, responses |

!!! info "Notices Service"
    The Notices service uses **in-memory caching** instead of a database, scraping data from the UIU website.

## Connection

All databases connect to Aiven PostgreSQL:

```
Host: pg-1ea37722-aranov1107-6aeb.c.aivencloud.com
Port: 16231
SSL: Required
```

## Population Order

Due to foreign key constraints, populate databases in this order:

1. **auth_db** (First) - Contains all user references
2. **market_db** (Second) - References user IDs
3. **rent_db** (Third) - References user IDs
