<!--
title: prowlarr
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# prowlarr

## Overview
Prowlarr aggregates Usenet and torrent indexers, providing unified API feeds for Radarr, Sonarr, and other download managers. Configuration lives under `/mnt/user/appdata/prowlarr`.【F:yarr/compose.yml†L119-L151】

## Runtime Profile
- **Image:** `ghcr.io/binhex/arch-prowlarr:latest`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/appdata/prowlarr:/config`
- **Environment:** PUID, PGID, timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Register indexers (Torznab/Newznab) and link them to Radarr/Sonarr using API keys.
- Combine with FlareSolverr for sites requiring anti-bot handling.
- Monitor update availability via WUD to keep indexer compatibility current.【F:devtools/compose.yml†L119-L176】
