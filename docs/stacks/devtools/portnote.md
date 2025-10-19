# portnote

## Overview
Portnote tracks infrastructure assets, ports, and credentials with OIDC protection from Authentik. It stores application state in the shared Postgres database and exposes its API/UI on `db_net` for internal access and proxied exposure.【F:devtools/compose.yml†L177-L210】

## Runtime Profile
- **Image:** `haedlessdev/portnote:latest`
- **Networks:** `db_net`
- **Environment:** Defines database URL (root credentials), HTTP port, JWT secrets, and login credentials injected from `.env`.
- **Healthcheck:** `wget` against `http://127.0.0.1:8080/` every 30 seconds.【F:devtools/compose.yml†L200-L209】
- **Labels:** Provide icon and WebUI metadata for Unraid.

## Integrations & Operations
- Authentik OIDC integration is enabled via environment variables; ensure the client is configured in Authentik with matching redirect URIs.【F:authentik/compose.yml†L24-L82】
- The companion `portnote-agent` container syncs data using the same Postgres credentials; rotate passwords carefully to avoid drift.
- Backup `portnote_data` volume through Autorestic to capture attachment exports.【F:devtools/compose.yml†L186-L200】
