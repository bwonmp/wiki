<!--
title: Tools Stack
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# Tools Stack

Productivity and automation services live in the Tools stack: document management, remote desktop, code editing, file browsing, recipe management, notifications, workflow automation, file synchronization, and PDF conversion.【F:tools/compose.yml†L1-L330】

## Topology Overview
- **Networks:** Combination of `frontend_net`, `backend_net`, and `db_net` depending on whether the service requires database access or public exposure.【F:tools/compose.yml†L5-L305】
- **Volumes:** Named volumes plus `/mnt/user` bind mounts hold data for Paperless, Mealie, FileBrowser, Syncthing, etc. Some volumes (e.g., `tools_new_filebrowser_config`) are external to preserve existing state.【F:tools/compose.yml†L10-L318】
- **Authentication:** Several services integrate with Authentik via OIDC (Paperless, Mealie, n8n) or rely on Authentik-protected frontends.

## Component Index

| Service | Role |
| --- | --- |
| [paperless](paperless.md) | Document ingestion and OCR repository backed by Postgres and Redis. |
| [firefox](firefox.md) | Headless Firefox browser accessible via noVNC. |
| [code-server](code-server.md) | VS Code in the browser for remote development. |
| [filebrowser](filebrowser.md) | Web-based file manager with access to `/mnt/user`. |
| [mealie](mealie.md) | Recipe manager with OIDC authentication. |
| [organizr](organizr.md) | Unified portal dashboard aggregating service links. |
| [apprise](apprise.md) | Notification relay API supporting many providers. |
| [n8n](n8n.md) | Workflow automation engine connected to Postgres and Redis. |
| [rclone](rclone.md) | Remote storage synchronization with optional web UI. |
| [syncthing](syncthing.md) | Continuous file synchronization across devices. |
| [bentopdf](bentopdf.md) | PDF conversion service. |

### Integration Notes
- Paperless and Mealie depend on the shared Postgres and Redis services; ensure credentials match the Databases stack configuration.【F:databases/compose.yml†L28-L70】
- n8n uses Redis DB 3 and Postgres; coordinate credentials when rotating secrets or changing hostnames.【F:tools/compose.yml†L208-L279】
- FileBrowser and Syncthing both expose `/mnt/user`; enforce permissions via PUID/PGID and user-level policies to prevent accidental data loss.
