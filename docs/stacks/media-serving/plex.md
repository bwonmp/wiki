# plex

## Overview
Primary Plex Media Server instance serving movies, TV, and 4K content. Runs in host network mode for DLNA discovery and broad client compatibility. Uses Intel QuickSync for hardware transcoding.【F:media_serving/compose.yml†L171-L205】

## Runtime Profile
- **Image:** `lscr.io/linuxserver/plex`
- **Network mode:** `host`
- **Volumes:**
  - `plex_config:/config`
  - `/mnt/user/Media/Movies:/movies`
  - `/mnt/user/Media/TV:/tv`
  - `/mnt/user/Media/4K_Movies:/4kmovies`
  - `/mnt/user/Media/4K_TV:/4ktv`
- **Environment:** `PUID`, `PGID`, `VERSION=docker`, timezone, `PLEX_CLAIM`
- **Devices:** `/dev/dri`

## Integrations & Operations
- Overseerr, Tautulli, Kometa, and other services in the Yarr/Monitoring stacks connect to Plex via HTTP and tokens.【F:yarr/compose.yml†L200-L420】【F:monitoring/compose.yml†L90-L160】
- Keep `PLEX_CLAIM` updated when migrating hosts; remove after successful claim to avoid re-registering.
- Backup `plex_config` to preserve library metadata and watch history.
