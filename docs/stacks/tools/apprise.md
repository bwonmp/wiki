# apprise

## Overview
Apprise API offers a unified notification gateway supporting dozens of providers (Discord, email, SMS). It stores configuration in `apprise_data` and exposes port 8000 internally.【F:tools/compose.yml†L279-L312】

## Runtime Profile
- **Image:** `lscr.io/linuxserver/apprise-api:latest`
- **Networks:** `frontend_net`
- **Volumes:** `apprise_data:/config`
- **Environment:** `PUID`, `PGID`, timezone
- **Healthcheck:** `wget http://127.0.0.1:8000/status`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Configure notifications for Paperless, Autorestic, and other services by pointing them to the Apprise endpoint.
- Manage configuration via `config.yaml` under the mounted volume.
- Secure the API behind Authentik or API keys if exposed outside the LAN.
