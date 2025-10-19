# fileflows

## Overview
FileFlows automates media file processing tasks such as transcoding, renaming, and cleaning. It mounts `/mnt/user/appdata/fileflows` for configuration and `/mnt/user` for media access.【F:yarr/compose.yml†L576-L610】

## Runtime Profile
- **Image:** `revenz/fileflows:stable`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/appdata/fileflows:/app/Data`, `/mnt/user:/media`
- **Healthcheck:** `wget http://127.0.0.1:5000/`
- **Environment:** timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Configure pipelines within FileFlows to handle post-download cleanup before Plex scans.
- Ensure `/media` mount has necessary permissions to modify files.
- Monitor CPU usage; heavy transcoding may impact Plex transcodes.
