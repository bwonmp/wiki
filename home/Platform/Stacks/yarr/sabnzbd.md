<!--
title: sabnzbd
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# sabnzbd

## Overview
SABnzbd handles Usenet downloads with automation support for Radarr/Sonarr. It runs on `frontend_net` and `backend_net` and mounts download directories plus configuration under `/mnt/user/appdata/sabnzbd`.【F:yarr/compose.yml†L41-L76】

## Runtime Profile
- **Image:** `lscr.io/linuxserver/sabnzbd:latest`
- **Networks:** `frontend_net`, `backend_net`
- **Volumes:** `/mnt/user/appdata/sabnzbd:/config`, `/mnt/tb/Downloads/completed:/downloads`, `/mnt/tb/Downloads/incomplete:/incomplete-downloads`, `/mnt/user/appdata/sabnzbd/scripts:/scripts`
- **Environment:** PUID/PGID, timezone
- **Labels:** Provide icon/WebUI metadata
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Connect to NZB indexers via API keys configured in the UI.
- Coordinate categories and folders with Radarr/Sonarr to trigger post-processing.
- Telegraf monitors SABnzbd via API key defined in `.env` for metrics shipping to InfluxDB.【F:monitoring/compose.yml†L255-L287】
