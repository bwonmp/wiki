# komga

## Overview
Komga manages comic libraries with web-based reading, metadata fetching, and user management. It mounts comics and configuration directories and exposes port 25600 for access.【F:media_serving/compose.yml†L267-L310】

## Runtime Profile
- **Image:** `gotson/komga`
- **Networks:** `frontend_net`
- **Ports:** `25600:25600`
- **Volumes:** `/mnt/user/Media/Comics/:/books/`, `/mnt/user/appdata/Komga:/config/`
- **Environment:** Timezone, `PUID`, `PGID`, optional servlet context path
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Initial password reset command is provided via `command` for first-run setup; remove after establishing admin credentials.
- Integrates with NetAlertX/Mylar for comic acquisition via shared directories.【F:yarr/compose.yml†L260-L360】
- Backup `/config` to retain metadata and reading progress.
