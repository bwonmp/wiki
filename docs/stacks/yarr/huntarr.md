# huntarr

## Overview
Huntarr aggregates search capabilities across Usenet and torrent sources, providing a unified UI for manual discovery. Data persists in the `huntarr_data` volume.【F:yarr/compose.yml†L611-L640】

## Runtime Profile
- **Image:** `huntarr/huntarr:latest`
- **Networks:** `backend_net`
- **Volumes:** `huntarr_data:/config`
- **Healthcheck:** `wget http://127.0.0.1:9705/`
- **Environment:** timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Connect to Prowlarr or direct indexers to broaden search coverage.
- Use to manually queue items not automatically picked up by Radarr/Sonarr.
