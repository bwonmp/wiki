# tunarr

## Overview
Tunarr creates virtual channels from Plex libraries to emulate live TV. It requires GPU access for transcoding and stores configuration in `/mnt/user/appdata/tunarr`.

## Runtime Profile
- **Image:** `ghcr.io/chrisbenincasa/tunarr:latest`
- **Networks:** `backend_net`
- **Ports:** `17442:8000`
- **Volumes:** `/mnt/user/appdata/tunarr:/config`
- **Devices:** `/dev/dri`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Configure channels through the web UI and point them to Plex libraries served by the `plex` container.
- Monitor GPU utilization and adjust channel counts to avoid saturating QuickSync resources.【F:media_serving/compose.yml†L35-L98】
- Back up `/config` via Autorestic or host-level snapshots.
