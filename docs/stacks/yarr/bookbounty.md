# bookbounty

## Overview
BookBounty automates ebook requests and downloads. It stores configuration under `/mnt/user/appdata/bookbounty` and watches `/mnt/user/Downloads` for completed items.【F:yarr/compose.yml†L791-L818】

## Runtime Profile
- **Image:** `thewicklowwolf/bookbounty:latest`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/appdata/bookbounty:/config`, `/mnt/user/Downloads:/downloads`
- **Environment:** PUID, PGID, timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Configure provider credentials to fetch ebooks from preferred sources.
- Coordinate with Readarr for import automation.
