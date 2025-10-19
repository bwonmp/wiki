# Monitoring Stack

Observability services aggregate metrics, logs, and smart device telemetry. Grafana provides dashboards, Loki handles logs, Alloy/Telegraf collect host metrics, and Netdata, Uptime Kuma, Scrutiny, and Tautulli add specialized views.【F:monitoring/compose.yml†L1-L215】

## Topology Overview
- **Networks:** Mix of `monitoring_net`, `backend_net`, `db_net`, and `frontend_net` depending on data sources and UI access.【F:monitoring/compose.yml†L5-L195】
- **Storage:** Each service uses persistent volumes (e.g., `grafana_data`, `loki_data`, `uptimekuma_data`, `scrutiny_*`, `influxdb_data`, `cloudbeaver_data`). Bind mounts provide host access (Docker socket, `/proc`, SMART data).【F:monitoring/compose.yml†L8-L205】
- **Security:** Several containers mount `/var/run/docker.sock`; restrict access to trusted services only.

## Component Index

| Service | Role |
| --- | --- |
| [grafana](grafana.md) | Dashboarding UI for metrics and logs. |
| [loki](loki.md) | Log aggregation backend. |
| [alloy](alloy.md) | Collector for metrics/logs feeding Loki/Grafana. |
| [uptime-kuma](uptime-kuma.md) | Synthetic monitoring and status page. |
| [scrutiny](scrutiny.md) | SMART drive monitoring with historical trends. |
| [tautulli](tautulli.md) | Plex usage analytics. |
| [homepage-tautulli-integration](homepage-tautulli-integration.md) | Lightweight API exposing Tautulli stats to Homepage dashboards. |
| [influxdb](influxdb.md) | Time-series database for IoT sensors. |
| [netdata](netdata.md) | Real-time host telemetry. |
| [telegraf](telegraf.md) | Agent forwarding metrics to InfluxDB and other sinks. |
| [glances](glances.md) | Alternative host monitoring accessible via web UI. |
| [cloudbeaver](cloudbeaver.md) | Web-based database client. |

### Integration Notes
- Tautulli and the Homepage integration depend on Plex being reachable; ensure tokens and URLs remain valid.【F:monitoring/compose.yml†L90-L140】【F:media_serving/compose.yml†L171-L205】
- Alloy reads `/var/lib/docker/containers` and the Docker socket; keep host log retention in mind to avoid disk bloat.
- Telegraf forwards metrics to InfluxDB (`INFLUX_TOKEN`) and queries Sonarr/Radarr/Sabnzbd via API keys provided in `.env`.【F:monitoring/compose.yml†L200-L239】【F:yarr/compose.yml†L200-L360】
