# changedetection

## Overview
Changedetection.io monitors webpages for content changes and can trigger notifications or workflows when differences are detected. Data persists under the `changedetection_data` volume to retain history and selectors.【F:devtools/compose.yml†L42-L69】

## Runtime Profile
- **Image:** `dgtlmoon/changedetection.io:latest`
- **Networks:** `backend_net`
- **Volumes:** `changedetection_data:/datastore`
- **Healthcheck:** Performs a Python socket check against `127.0.0.1:5000` with retries to ensure the web server is responsive.【F:devtools/compose.yml†L58-L67】
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Exposed internally on port 5000; publish via Nginx Proxy Manager if remote access is required.
- Autorestic includes the datastore volume in its backup manifest; monitor job logs for completion status.【F:devtools/compose.yml†L186-L200】
- For Discord or Apprise alerts, configure webhooks from the Tools stack’s `apprise` service.
