<!--
title: whatsupdocker
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# whatsupdocker

## Overview
What’s Up Docker (WUD) monitors Docker registries and running containers, alerting you to available updates. It authenticates against Docker Hub, GHCR, and LinuxServer registries and exposes a web UI plus HTTP triggers for automation.【F:devtools/compose.yml†L119-L176】

## Runtime Profile
- **Image:** `getwud/wud:latest`
- **Networks:** `backend_net`
- **Volumes:** `/var/run/docker.sock`, `wud_data:/store`
- **Environment:** Extensive configuration defining watchers, registry credentials, auto-update thresholds, Discord webhooks, and architecture filters.【F:devtools/compose.yml†L128-L169】
- **Healthcheck:** `curl` to `/api/health` every 30 seconds with retries.【F:devtools/compose.yml†L170-L176】

## Integrations & Operations
- Sends notifications to the custom Discord bot via HTTP triggers when major updates are available.【F:devtools/compose.yml†L152-L167】
- Autorestic backs up `wud_data` nightly; confirm the volume retains tag history after container upgrades.【F:devtools/compose.yml†L186-L200】
- Requires Docker socket access; ensure host security posture allows privileged reads from `/var/run/docker.sock`.
