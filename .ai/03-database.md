# Database Conventions

## 1. Core Engine
- **Database:** [e.g., PostgreSQL via Supabase]
- **Schema Management:** Versioned SQL migrations (do not use ORM auto-push in production).

## 2. Row Level Security (RLS)
- All tables must have RLS enabled by default.
- Write explicit policies for `SELECT`, `INSERT`, `UPDATE`, and `DELETE`.
- The default stance is `DENY ALL`. Access must be explicitly granted based on authenticated roles.

## 3. Identity Governance
- Use database triggers to sync authentication provider roles (e.g., JWT claims) to public profile tables.
