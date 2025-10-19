# telegraf

## Overview
Telegraf collects metrics from the host, Docker, and media applications, forwarding them to InfluxDB. It runs in host PID mode with multiple bind mounts for system metrics.【F:monitoring/compose.yml†L255-L287】

## Runtime Profile
- **Image:** `telegraf:1.30-alpine`
- **Networks:** `frontend_net`, `backend_net`, `db_net`
- **Volumes:** `/var/run/docker.sock`, `/mnt/user/appdata/telegraf/telegraf.conf`, `/proc`, `/sys`, `/var/run/utmp`, root filesystem read-only
- **Environment:** `INFLUX_TOKEN`, host name, API keys for SABnzbd, Radarr, Sonarr
- **Command:** `telegraf --config /etc/telegraf/telegraf.conf`
- **Restart policy:** default (not specified)

## Integrations & Operations
- Update `telegraf.conf` with input plugins for new services; reload container after edits.
- Keep API keys in sync with Yarr stack downloaders when rotated.【F:yarr/compose.yml†L200-L360】
- Ensure InfluxDB token has write access to the designated bucket.
