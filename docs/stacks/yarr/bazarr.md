# bazarr

## Overview
Bazarr fetches and manages subtitles for Radarr/Sonarr libraries. It mounts movie and TV directories to ensure subtitles stay alongside media files.【F:yarr/compose.yml†L303-L340】

## Runtime Profile
- **Image:** `lscr.io/linuxserver/bazarr:latest`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/appdata/bazarr:/config`, `/mnt/user/Media/Movies:/movies`, `/mnt/user/Media/TV:/tv`, `/mnt/user/Media/Movies:/mnt/movies`
- **Environment:** PUID, PGID, timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Provide Radarr/Sonarr API keys so Bazarr can track wanted releases.
- Configure language profiles to match media consumption preferences.
- Monitor disk usage for downloaded subtitles; prune duplicates as needed.
