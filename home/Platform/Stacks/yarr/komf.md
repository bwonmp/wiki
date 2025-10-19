<!--
title: komf
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# komf

## Overview
Komf fetches manga metadata and relies on FlareSolverr for bypassing Cloudflare. It runs on `backend_net` and exposes an actuator health endpoint consumed by the compose healthcheck.【F:yarr/compose.yml†L372-L409】

## Runtime Profile
- **Image:** `sndxr/komf:latest`
- **Networks:** `backend_net`
- **Environment:** timezone, `FLARESOLVERR_URL`
- **Healthcheck:** `wget http://127.0.0.1:8080/actuator/health`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Ensure FlareSolverr stays reachable; Komf fails queries without it.
- Configure manga sources via the Komf UI.
- Reverse proxy via NPM if remote access is required.
