# homepage-tautulli-integration

## Overview
Provides a lightweight API translating Tautulli stats for the Homepage dashboard. Runs on `monitoring_net` and exposes port 3002 (mapped to 3032) for consumption by Homepage widgets.【F:monitoring/compose.yml†L185-L205】

## Runtime Profile
- **Image:** `ghcr.io/10mfox/gethomepage-tautulli-custom-api:latest`
- **Ports:** `3032:3002`
- **Networks:** `monitoring_net`
- **Environment:** `TAUTULLI_API_KEY`, `TAUTULLI_URL`, `PORT`
- **Depends on:** `tautulli`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Update the API key and URL if Tautulli credentials change.
- Adjust the exposed port if multiple dashboards consume the service to avoid collisions.
