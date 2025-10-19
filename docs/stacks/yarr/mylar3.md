# mylar3

## Overview
Mylar3 automates comic downloads, renaming, and organization. It mounts comics, downloads, and torrent monitoring directories to coordinate with other automation tools.【F:yarr/compose.yml†L410-L449】

## Runtime Profile
- **Image:** `lscr.io/linuxserver/mylar3:latest`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/appdata/mylar3:/config`, `/mnt/user/Media/Comics:/comics`, `/mnt/user/Downloads:/downloads`, `/mnt/user/Downloads/torrents/monitor:/torrents`
- **Healthcheck:** `wget http://127.0.0.1:8090/`
- **Environment:** PUID, PGID, timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Integrate with NZB/torrent clients for automated downloads.
- Configure metadata providers inside the UI for cover art.
- Align library paths with Komga to keep reading apps updated.
