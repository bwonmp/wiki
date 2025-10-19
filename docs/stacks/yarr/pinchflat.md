# pinchflat

## Overview
Pinchflat downloads YouTube content according to playlists and integrates with Plex for library updates. It stores configuration under `/mnt/user/appdata/pinchflat` and saves downloads into TV library directories.【F:yarr/compose.yml†L485-L517】

## Runtime Profile
- **Image:** `ghcr.io/kieraneglin/pinchflat:latest`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/appdata/pinchflat:/config`, `/mnt/user/Media/TV:/downloads`
- **Environment:** timezone, `PF_USERNAME`, `PF_PASSWORD`, `ENABLE_PROMETHEUS`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Secure the web UI with credentials set in environment variables.
- Configure Plex notification hooks within Pinchflat to trigger library scans.
- Monitor Prometheus endpoint if integrating with Grafana.
