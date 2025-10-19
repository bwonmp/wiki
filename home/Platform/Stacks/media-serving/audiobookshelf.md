<!--
title: audiobookshelf
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# audiobookshelf

## Overview
Audiobookshelf streams audiobooks and podcasts with multi-user support. It leverages ThemePark for theming and mounts libraries plus configuration directories from the host.【F:media_serving/compose.yml†L69-L113】

## Runtime Profile
- **Image:** `ghcr.io/advplyr/audiobookshelf`
- **Networks:** `frontend_net`, `backend_net`
- **Volumes:**
  - `/mnt/user/Media/Audiobooks/:/audiobooks`
  - `/mnt/user/appdata/audiobookshelf/metadata/:/metadata`
  - `/mnt/user/appdata/audiobookshelf/config/:/config`
- **Environment:** `DOCKER_MODS=ghcr.io/themepark-dev/theme.park:overseer`, timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Expose via NPM under `audiobooks.bryanwank.com`; consider adding Authentik for OIDC login.
- Works with `abs-autoconverter` in the Yarr stack for format conversions—coordinate library paths accordingly.【F:yarr/compose.yml†L520-L610】
- Backup config and metadata directories to preserve user progress and metadata.
