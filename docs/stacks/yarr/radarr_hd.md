# radarr_hd

## Overview
Radarr HD manages the primary 1080p movie library, orchestrating downloads via SABnzbd/Deluge and sending completed media to Plex libraries.【F:yarr/compose.yml†L152-L193】

## Runtime Profile
- **Image:** `hotio/radarr:latest`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/appdata/radarr_hd:/config`, `/mnt/user/Media/Movies:/mnt/movies`, `/mnt/tb/Downloads/completed:/downloads`
- **Environment:** PUID, PGID, timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Connect to SABnzbd/Deluge via download client settings.
- API key shared with Telegraf for monitoring metrics; update `.env` when rotating keys.【F:monitoring/compose.yml†L255-L287】
- Use Custom Formats and Quality Profiles to manage import rules.
