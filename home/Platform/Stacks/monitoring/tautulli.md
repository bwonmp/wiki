<!--
title: tautulli
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# tautulli

## Overview
Tautulli tracks Plex usage, stream history, and notifications. It mounts configuration under `/mnt/user/appdata/tautulli` and exposes the UI on `8141:8181`.【F:monitoring/compose.yml†L159-L185】

## Runtime Profile
- **Image:** `tautulli/tautulli:latest`
- **Ports:** `8141:8181`
- **Networks:** `monitoring_net`, `backend_net`
- **Volumes:** `/mnt/user/appdata/tautulli:/config`
- **Environment:** `PUID`, `PGID`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Provide the Plex token and URL within Tautulli to enable API access.
- Homepage integration consumes Tautulli’s API; keep the API key in sync with `TAUTULLI_API_KEY` used by the integration container.【F:monitoring/compose.yml†L185-L205】
- Backup configuration to preserve notification rules and history.
