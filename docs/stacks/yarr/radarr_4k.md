# radarr_4k

## Overview
Radarr 4K mirrors the configuration of [radarr_hd](radarr_hd.md) but targets the 4K movie library. It points to `/mnt/user/Media/4K_Movies/Movies` for imports while sharing completed download directories.【F:yarr/compose.yml†L194-L219】

## Runtime Profile
- **Image:** `hotio/radarr:latest`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/appdata/radarr_4k:/config`, `/mnt/user/Media/4K_Movies/Movies:/mnt/movies`, `/mnt/tb/Downloads/completed:/downloads`
- **Environment:** PUID, PGID, timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Configure separate quality profiles and root folders for 4K content.
- Share API keys carefully; monitoring integrations should distinguish between HD/4K instances if needed.
