# maintainerr

## Overview
Maintainerr automates cleanup tasks in Plex libraries, such as deleting watched content or applying naming standards. It stores state under `/mnt/user/appdata/maintainerr`.【F:yarr/compose.yml†L859-L878】

## Runtime Profile
- **Image:** `ghcr.io/jorenn92/maintainerr:latest`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/appdata/maintainerr:/opt/data`
- **Environment:** timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Configure Plex connection details and automation rules through the UI.
- Coordinate with Kometa and Plex-Hub-Manager to avoid conflicting automation.
