# ultimate-audiobooks

## Overview
Utility container providing a bash environment with scripts for managing audiobook libraries. It mounts source code, audiobook library, and download directories for manual operations.【F:yarr/compose.yml†L879-L910】

## Runtime Profile
- **Image:** `python:3.12-slim`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/appdata/ultimate-audiobooks:/app`, `/mnt/user/Media/Audiobooks:/audiobooks`, `/mnt/user/Downloads/completed/AudioBooks:/downloads`
- **Entry:** `bash` with TTY enabled
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Use for running scripts that normalize audiobook metadata or structure before importing into Audiobookshelf.
- Since it’s interactive, manage processes manually; consider adding cron tasks if automation is required.
