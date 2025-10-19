<!--
title: glances
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# glances

## Overview
Glances offers an alternative host monitoring interface accessible via web UI. Running in host network mode with PID namespace access, it reads system metrics directly and exposes them through a lightweight server.【F:monitoring/compose.yml†L287-L309】

## Runtime Profile
- **Image:** `nicolargo/glances:ubuntu-latest-full`
- **Network mode:** `host`
- **Volumes:** `/var/run/docker.sock`, `/run/user/1000/podman/podman.sock`
- **Environment:** `GLANCES_OPT=-w`
- **Restart policy:** default (not specified)

## Integrations & Operations
- Access via `http://<host>:61208` (default) when running; ensure port is not blocked by firewall.
- Useful for quick troubleshooting when Grafana/Netdata dashboards are not available.
