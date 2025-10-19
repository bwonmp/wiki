<!--
title: netdata
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# netdata

## Overview
Netdata provides real-time host monitoring with minimal configuration. It runs in host mode to collect kernel metrics, Docker stats, and hardware telemetry.【F:monitoring/compose.yml†L222-L255】

## Runtime Profile
- **Image:** `netdata/netdata:latest`
- **Ports:** `19989:19999`
- **Networks:** `monitoring_net`, `backend_net`
- **Volumes:**
  - `/proc:/host/proc:ro`
  - `/sys:/host/sys:ro`
  - `/var/run/docker.sock:/var/run/docker.sock:ro`
  - `/mnt/user/appdata/netdata/config:/etc/netdata:rw`
  - `/mnt/user/appdata/netdata/lib:/var/lib/netdata:rw`
  - `/mnt/user/appdata/netdata/cache:/var/cache/netdata:rw`
- **Capabilities:** `SYS_PTRACE`, `apparmor:unconfined`

## Integrations & Operations
- Access at `http://<host>:19989` for dashboards.
- Configure streaming/export to InfluxDB or Prometheus if long-term retention is needed.
- Ensure mount points remain read/write to allow Netdata to persist configuration and historical data.
