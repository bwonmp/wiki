<!--
title: Authentik Stack
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# Authentik Stack

The Authentik stack delivers centralized identity, access management, and reverse-proxy enforcement for the rest of the platform. It runs the primary Authentik application, a background worker tier, and two proxy outposts that enforce authentication for downstream services published through Nginx Proxy Manager.

## Topology Overview

- **Networks:** `frontend_net` for browser access, `backend_net` for cross-stack callbacks, and `db_net` for database access.【F:authentik/compose.yml†L5-L37】
- **Data Services:** Relies on the shared PostgreSQL and Redis instances provided by the Databases stack.【F:authentik/compose.yml†L25-L60】【F:databases/compose.yml†L11-L95】
- **Stateful Storage:** Shared template and media volumes (`ak_templates`, `ak_media`) preserve branding assets and exported flows across upgrades.【F:authentik/compose.yml†L12-L18】【F:authentik/compose.yml†L37-L44】
- **Tokens & Secrets:** Environment variables reference `.env` secrets for database credentials, Redis passwords, and outpost tokens to keep sensitive values out of source control.【F:authentik/compose.yml†L28-L81】

## Component Index

| Service | Role |
| --- | --- |
| [authentik-server](authentik-server.md) | Web application tier that hosts the Authentik admin UI, identity flows, and OAuth/OIDC providers. |
| [authentik-worker](authentik-worker.md) | Background worker executing asynchronous policy checks, directory sync, and email pipelines. |
| [ak-outpost-organizr](ak-outpost-organizr.md) | Reverse-proxy outpost that injects SSO in front of Organizr and other frontend applications. |
| [ak-outpost-cwad](ak-outpost-cwad.md) | Embedded Authentik proxy used by Calibre-Web Automated Downloader and similar backend services. |

### Integration Notes

- Authentik issues OIDC tokens that are consumed by Paperless, Mealie, Portnote, and other stacks documented elsewhere.【F:tools/compose.yml†L26-L177】【F:devtools/compose.yml†L120-L187】
- The outposts must stay on the same Docker networks as the protected applications (e.g., `frontend_net` with Nginx Proxy Manager, `backend_net` with CWAD) to terminate requests before they reach the upstream container.【F:authentik/compose.yml†L62-L81】
- Backup the media and template volumes via the Autorestic job in the Dev Tools stack to retain custom branding and flow exports.【F:devtools/compose.yml†L186-L238】
