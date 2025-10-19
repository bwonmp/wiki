# overseerr

## Overview
Overseerr handles media requests, integrates with Plex, and triggers Radarr/Sonarr to add new content. It joins both `frontend_net` and `backend_net` to serve the UI and reach automation services.【F:yarr/compose.yml†L341-L371】

## Runtime Profile
- **Image:** `sctx/overseerr:latest`
- **Networks:** `frontend_net`, `backend_net`
- **Volumes:** `/mnt/user/appdata/overseerr:/app/config`
- **Environment:** timezone, `LOG_LEVEL`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Connect to Plex via token to display library and request history.
- Configure Radarr/Sonarr/SABnzbd endpoints in the UI.
- Add Authentik or reverse proxy protection if exposing externally.
