<!--
title: alloy
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# alloy

## Overview
Alloy (Grafana Agent successor) scrapes metrics, collects logs, and forwards them to Grafana Cloud-compatible backends. It mounts the Docker socket and container logs for comprehensive telemetry.【F:monitoring/compose.yml†L60-L89】

## Runtime Profile
- **Image:** `grafana/alloy:latest`
- **Ports:** `12345:12345`
- **Networks:** `monitoring_net`, `backend_net`, `db_net`
- **Volumes:**
  - `/var/run/docker.sock:/var/run/docker.sock:ro`
  - `/var/lib/docker/containers:/var/lib/docker/containers:ro`
  - `/mnt/user/appdata/alloy/config.alloy:/etc/alloy/config.alloy:ro`
  - `/mnt/user/appdata/alloy/data:/var/lib/alloy/data`
- **Command:** `run --server.http.listen-addr=0.0.0.0:12345 --storage.path=/var/lib/alloy/data /etc/alloy/config.alloy`

## Integrations & Operations
- Configure pipelines within `config.alloy` to send metrics/logs to Loki and Prometheus-compatible endpoints.
- Requires read access to container logs; ensure host path retention meets your observability requirements.
- Monitor disk usage of `/var/lib/alloy/data` and prune old segments if necessary.
