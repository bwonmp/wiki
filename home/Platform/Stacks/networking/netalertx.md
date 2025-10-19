<!--
title: netalertx
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# netalertx

## Overview
NetAlertX monitors devices on the local network, detecting new hosts and outages. It runs in host network mode for full LAN visibility and stores configuration in `netalertx_data`.【F:networking/compose.yml†L48-L84】

## Runtime Profile
- **Image:** `jokobsk/netalertx:latest`
- **Network mode:** `host`
- **Volumes:** `netalertx_data:/app/data`
- **Environment:** Timezone and optional interface settings
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Optionally mount Pi-hole’s `pihole-FTL.db` read-only to enrich device metadata.
- Configure notifications within NetAlertX for Discord, email, or webhook alerts.
- Access UI at `http://<host>:20211` unless proxied via NPM.
