# Security & Guardrails

## 1. Zero-Leak Policy
- Never expose service-role keys, database passwords, or third-party API secret keys in client-side code.
- All environment variables used in client bundles must be explicitly whitelisted (e.g., prefixed with `PUBLIC_` or `VITE_`).

## 2. PII Handling (Personally Identifiable Information)
- Do not write queries that use `SELECT *` on tables containing PII.
- Always explicitly select public-safe fields.
- Assume all user data is sensitive unless explicitly marked public.

## 3. Destructive Operations
- Always ask for human confirmation before executing `DROP TABLE`, `DELETE` without a strict `WHERE` clause, or force-pushing git branches.
- Never write migration scripts that drop columns without a fallback plan.
