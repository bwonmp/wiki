<!--
title: firefox
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# firefox

## Overview
Headless Firefox container delivers a browser via noVNC for testing or accessing web resources from within the homelab network. Configuration persists under `firefox_config`.【F:tools/compose.yml†L85-L121】

## Runtime Profile
- **Image:** `lscr.io/linuxserver/firefox:latest`
- **Networks:** `frontend_net`
- **Ports:** exposed via reverse proxy (internal 3000/8082)
- **Volumes:** `firefox_config:/config`
- **Environment:** `PUID`, `PGID`, timezone, DNS override
- **Healthcheck:** `curl`/`nc` checks against ports 3000 and 8082
- **Restart policy:** `no` (manual control)

## Integrations & Operations
- Use NPM to publish the noVNC interface securely; consider Authentik to restrict access.
- Increase `shm_size` if pages require more shared memory.
- For automation, mount additional volumes with profiles or use Selenium over VNC.
