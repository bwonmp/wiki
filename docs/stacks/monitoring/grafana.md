# grafana

## Overview
Grafana is the visualization layer for metrics and logs collected from InfluxDB, Loki, Telegraf, and Alloy. It exposes the UI on port 3000 (mapped to 3014 on the host) and stores dashboards in `grafana_data`.【F:monitoring/compose.yml†L1-L28】

## Runtime Profile
- **Image:** `grafana/grafana:latest`
- **Ports:** `3014:3000`
- **Networks:** `monitoring_net`, `backend_net`, `db_net`
- **Volumes:** `grafana_data:/var/lib/grafana`
- **Environment:** Admin credentials (`GF_SECURITY_ADMIN_USER/PASSWORD`), `PUID`, `PGID`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Configure data sources for InfluxDB (`http://influxdb:8086`) and Loki (`http://loki:3100`) after deployment.【F:monitoring/compose.yml†L200-L239】
- Secure the admin account immediately—Grafana defaults to simple credentials.
- Backup `grafana_data` to preserve dashboards, alert rules, and plugins.
