<!--
title: Media Serving Stack
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# Media Serving Stack

This stack powers the entertainment library—books, audiobooks, comics, ROMs, Plex, and related automation utilities. Services span multiple networks to isolate database access, backend processing, and public interfaces.【F:media_serving/compose.yml†L1-L210】

## Topology Overview
- **Networks:** Mix of `frontend_net`, `backend_net`, and `db_net` depending on whether the service needs public exposure or database connectivity.【F:media_serving/compose.yml†L7-L188】
- **Storage:** Extensive bind mounts into `/mnt/user/Media`, `/mnt/user/Downloads`, and `/mnt/user/appdata` hold libraries and configuration. Named volumes capture container-specific data (e.g., `romm_resources`, `plex_config`).【F:media_serving/compose.yml†L14-L205】
- **Hardware:** Several containers leverage `/dev/dri` for transcoding (Plex, Tunarr, Storyteller). Ensure Intel QuickSync drivers remain available on the host.【F:media_serving/compose.yml†L38-L98】【F:media_serving/compose.yml†L160-L190】

## Component Index

| Service | Role |
| --- | --- |
| [booklore](booklore.md) | Modern book server with metadata ingestion and optional OIDC auth. |
| [tunarr](tunarr.md) | Virtual live TV channel generator integrating with Plex. |
| [calibre](calibre.md) | Desktop Calibre environment accessible via noVNC. |
| [audiobookshelf](audiobookshelf.md) | Audiobook library and streaming server. |
| [calibre-web-automated](calibre-web-automated.md) | Automation wrapper around Calibre-Web for ingest workflows. |
| [romm](romm.md) | Retro ROM library manager connected to MariaDB. |
| [plex](plex.md) | Primary Plex Media Server instance. |
| [plex-hub-manager](plex-hub-manager.md) | Automates Plex hubs/collections. |
| [tinfoil](tinfoil.md) | Nintendo Switch NSP distribution helper. |
| [storyteller](storyteller.md) | Audiobook/ebook platform with GPU acceleration. |
| [komga](komga.md) | Comic library server. |

### Integration Notes
- RomM, Booklore, and Calibre Web rely on the Databases stack (MariaDB) for relational data; confirm credentials align with `mariadb` service users.【F:media_serving/compose.yml†L1-L165】【F:databases/compose.yml†L72-L95】
- Plex and Tunarr share GPU resources; monitor `intel_gpu_top` to avoid resource contention during transcodes.
- Storyteller and Calibre-Web ingest content from the same directories as Calibre and Booklore—coordinate automation to prevent duplicate imports.
