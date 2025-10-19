<!--
title: authentik-server
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# authentik-server

## Overview
The primary Authentik application container serves the administrative UI, identity provider endpoints, and policy engines. It exposes the `/server` command entrypoint, stores uploaded media and templates on dedicated volumes, and brokers authentication flows for downstream services published through Nginx Proxy Manager.【F:authentik/compose.yml†L19-L45】

## Runtime Profile
- **Image:** `ghcr.io/goauthentik/server:2025.8.4`
- **Command:** `server`
- **Restart policy:** `unless-stopped`
- **Volumes:** `ak_media:/media`, `ak_templates:/templates`
- **Networks:** `frontend_net`, `backend_net`, `db_net`
- **Health:** Utilizes Redis and PostgreSQL readiness; no explicit healthcheck is defined in compose.

## Configuration & Secrets
Key environment variables are sourced from the stack `.env` file:

| Variable | Purpose |
| --- | --- |
| `AUTHENTIK_SECRET_KEY` | Core application signing key. |
| `AUTHENTIK_POSTGRESQL__HOST/PORT/NAME/USER/PASSWORD` | Database connectivity routed to the shared `postgres` container on `db_net`. |
| `AUTHENTIK_REDIS__HOST/PORT/DB/PASSWORD` | Session and cache backend hosted on the shared `redis` service. |
| `AUTHENTIK_COOKIE_DOMAIN` / `AUTHENTIK_HOST` | Public URLs that must match DNS used by `frontend_net` applications. |
| `POSTGRES_PASSWORD` | Legacy variable retained for compatibility with Authentik migrations. |

All sensitive values (`*_PASSWORD`, tokens) are expected to be injected through the environment rather than committed to source control.【F:authentik/compose.yml†L24-L56】

## Integrations
- Depends on the Databases stack for PostgreSQL and Redis availability before boot; the `depends_on` clause ensures sequencing with those containers.【F:authentik/compose.yml†L46-L58】
- Issues OIDC tokens consumed by Paperless, Mealie, Portnote, and other applications that redirect back to `AUTHENTIK_HOST`. Review those stack pages before rotating URLs or secrets.【F:tools/compose.yml†L26-L177】【F:devtools/compose.yml†L120-L187】
- Shares template/media volumes with the outpost containers; Autorestic backs up these volumes nightly.【F:authentik/compose.yml†L12-L18】【F:devtools/compose.yml†L186-L238】

## Operational Notes
- Configure the Web UI at `https://auth.bryanwank.com` via the reverse proxy defined in the Frontdoor stack.
- Keep the container synchronized with the worker; update tags in tandem to avoid schema drift between background jobs and the API.
- When restoring from backup, ensure `AUTHENTIK_SECRET_KEY` remains constant so existing sessions remain valid.
