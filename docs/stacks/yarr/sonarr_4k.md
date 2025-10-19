# sonarr_4k

## Overview
Sonarr 4K mirrors [sonarr_hd](sonarr_hd.md) but targets the 4K TV library, mapping `/mnt/user/Media/4K_TV/TV` for imports while sharing downloads from SABnzbd/Deluge.【F:yarr/compose.yml†L260-L302】

## Runtime Profile
- **Image:** `ghcr.io/binhex/arch-sonarr:latest`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/appdata/sonarr_4k:/config`, `/mnt/user/Media:/media`, `/mnt/user/Media/4K_TV/TV:/4ktv`, `/mnt/tb/Downloads/completed:/downloads`
- **Environment:** PUID, PGID, timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Maintain distinct quality profiles for UHD sources.
- Provide API key updates to monitoring agents when rotating credentials.
