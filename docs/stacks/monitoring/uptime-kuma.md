# uptime-kuma

## Overview
Uptime Kuma provides synthetic monitoring and status pages for internal and external services. Data persists in `uptimekuma_data` and the web UI is exposed via `3013:3001`.【F:monitoring/compose.yml†L90-L122】

## Runtime Profile
- **Image:** `louislam/uptime-kuma:latest`
- **Ports:** `3013:3001`
- **Networks:** `backend_net`, `db_net`, `frontend_net`
- **Volumes:** `uptimekuma_data:/app/data`
- **Environment:** `PUID`, `PGID`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Configure monitors for Grafana, Nginx Proxy Manager, Immich, etc. using Docker network hostnames.
- Use Authentik or built-in authentication to protect the dashboard if exposed publicly.
- Backup `uptimekuma_data` to retain monitors and history.
