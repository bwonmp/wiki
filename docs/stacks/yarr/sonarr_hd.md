# sonarr_hd

## Overview
Sonarr HD manages 1080p TV series, coordinating with SABnzbd/Deluge and Plex libraries. It mounts TV library directories and completed downloads for import.【F:yarr/compose.yml†L220-L259】

## Runtime Profile
- **Image:** `ghcr.io/binhex/arch-sonarr:latest`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/appdata/sonarr_hd:/config`, `/mnt/user/Media:/media`, `/mnt/user/Media/TV:/tv`, `/mnt/tb/Downloads/completed:/downloads`
- **Environment:** PUID, PGID, timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Link to radarr, prowlarr, and download clients using API keys.
- Provide API key to Telegraf for monitoring as defined in `.env`.
- Use release profiles to prefer specific sources or languages.
