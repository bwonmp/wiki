# wikijs

## Overview
Wiki.js provides collaborative documentation with Git-backed version control. It connects to the shared PostgreSQL instance and exposes its UI on `frontend_net` while staying on `db_net` for database access.【F:devtools/compose.yml†L70-L118】

## Runtime Profile
- **Image:** `requarks/wiki:2`
- **Networks:** `frontend_net`, `db_net`
- **Volumes:** `wikijs_data:/wiki`
- **Environment:** Configures PostgreSQL host/port/user/password, DB name, timezone, and disables SSL for internal Docker communications.
- **Healthcheck:** Uses `wget http://127.0.0.1:3000/` to confirm the UI is responsive before reporting healthy.【F:devtools/compose.yml†L88-L100】

## Integrations & Operations
- Reverse proxy through Nginx Proxy Manager to present the wiki on a friendly hostname; secure with Authentik if required.
- Include the `wikijs_data` volume in backup routines via Autorestic.【F:devtools/compose.yml†L186-L200】
- Monitor Postgres performance; heavy use of page history increases database size quickly.
