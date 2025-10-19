# paperless

## Overview
Paperless-NGX ingests scanned documents, performs OCR, and stores metadata in Postgres with Redis caching. It supports Authentik OIDC for authentication and exposes HTTP on port 8000 (mapped to 8081).【F:tools/compose.yml†L25-L84】

## Runtime Profile
- **Image:** `ghcr.io/paperless-ngx/paperless-ngx:latest`
- **Ports:** `8081:8000`
- **Networks:** `frontend_net`, `db_net`
- **Volumes:** `paperless_data`, `paperless_media`, `paperless_consume`, `/mnt/user/Paperless/export`
- **Environment:** Database connection (`PAPERLESS_DB*`), Redis URL, allowed hosts, OIDC provider JSON, timezone/PUID/PGID
- **Healthcheck:** `curl http://127.0.0.1:8000/`

## Integrations & Operations
- Ensure Postgres (`paperless` user) and Redis (DB 2) credentials match the Databases stack.【F:databases/compose.yml†L28-L70】
- Configure Authentik provider with the specified redirect URIs; update environment if the domain changes.
- Autorestic backs up Paperless volumes; verify `.autorestic.yml` includes the relevant paths.【F:devtools/compose.yml†L186-L200】
