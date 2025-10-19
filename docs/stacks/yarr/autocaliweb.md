# autocaliweb

## Overview
Autocaliweb streamlines Calibre library management with a web UI. It mounts multiple directories for books, ingest, and existing Calibre data and exposes HTTP on port 5021.【F:yarr/compose.yml†L676-L712】

## Runtime Profile
- **Image:** `gelbphoenix/autocaliweb:latest`
- **Networks:** `frontend_net`
- **Ports:** `5021:8083`
- **Volumes:** `/mnt/user/appdata/autocaliweb_data:/data`, `/mnt/user/Downloads/completed/Books:/cwa-book-ingest`, `/mnt/user/Media/Calibre:/old_books`, `/mnt/user/Media/Books_fresh:/books`
- **Environment:** timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Coordinates with Calibre-Web Automated and CWAD; ensure ingest directories remain consistent.
- Protect via Authentik if exposing beyond LAN.
