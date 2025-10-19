# organizr

## Overview
Organizr aggregates links to services into a single dashboard, often protected by Authentik. It stores configuration in `organizr_config` and listens on internal port 80 (mapped to 7080).【F:tools/compose.yml†L246-L278】

## Runtime Profile
- **Image:** `organizr/organizr`
- **Networks:** `frontend_net`
- **Ports:** `7080:80`
- **Volumes:** `organizr_config:/config`
- **Environment:** `PUID`, `PGID`, timezone
- **Healthcheck:** `curl http://127.0.0.1`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Typically fronted by Authentik outpost (`ak-outpost-organizr`) for SSO enforcement.【F:authentik/compose.yml†L62-L76】
- Customize tabs to link to Grafana, Plex, Paperless, etc.
- Backup configuration to preserve custom themes and layout.
