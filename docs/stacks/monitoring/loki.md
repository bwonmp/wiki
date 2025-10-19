# loki

## Overview
Loki ingests logs from Alloy and other collectors, storing them for query via Grafana. Configuration mounts from `/mnt/user/appdata/loki`, enabling custom pipelines.【F:monitoring/compose.yml†L29-L59】

## Runtime Profile
- **Image:** `grafana/loki:3.5.3`
- **Ports:** `3112:3100`
- **Networks:** `monitoring_net`, `backend_net`, `db_net`
- **Volumes:** `/mnt/user/appdata/loki:/etc/loki`
- **Command:** `-config.file=/etc/loki/local-config.yaml -config.expand-env=true`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Pair with Alloy to collect container logs via the Docker socket.【F:monitoring/compose.yml†L60-L89】
- Ensure retention policies are tuned to available disk space; edit `local-config.yaml` to adjust chunk and index directories.
- Expose the API to Grafana through `http://loki:3100` when configuring the data source.
