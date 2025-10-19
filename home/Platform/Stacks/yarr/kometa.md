<!--
title: kometa
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# kometa

## Overview
Kometa automates Plex metadata management, generating collections, posters, and overlays based on YAML configuration. It mounts `kometa_data` for config storage.【F:yarr/compose.yml†L641-L675】

## Runtime Profile
- **Image:** `kometateam/kometa:latest`
- **Networks:** `backend_net`
- **Volumes:** `kometa_data:/config`
- **Command:** `/config/config.yml`
- **Healthcheck:** Ensures config file exists
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Configure Plex token and libraries inside `config.yml`.
- Schedule cron or container restarts to trigger metadata refreshes.
- Works alongside Plex-Hub-Manager; coordinate responsibilities to avoid conflicting edits.
