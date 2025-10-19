# crowdsec

## Overview
CrowdSec ingests HTTP access logs produced by Nginx Proxy Manager to detect brute-force attempts, credential stuffing, and other anomalies. When it identifies an offender, it records the decision in its local API (LAPI), which bouncers can query to block subsequent requests.【F:crowdsec/compose.yml†L12-L27】

## Runtime Profile
- **Image:** `crowdsecurity/crowdsec`
- **Ports:** `2291:8080` (exposes LAPI on the host for bouncers and dashboards)
- **Volumes:**
  - `/var/lib/docker/volumes/frontdoor_npm_data/_data/logs/` → `/var/log/nginx`
  - `/etc/crowdsec/config` → `/etc/crowdsec`
  - `/crowdsec/data` → `/var/lib/crowdsec/data`
- **Networks:** `backend_net`
- **Restart policy:** `always`

## Configuration
- `COLLECTIONS` loads the `crowdsecurity/nginx` parser pack tailored to reverse-proxy logs.
- `GID` ensures the container writes data with the desired group permissions for Unraid.
- Additional API keys for bouncers can be generated with `cscli bouncers add <name>` inside the container shell.

## Integrations & Operations
- Pair with the optional nginx bouncer (commented in compose) or with Authentik outpost middlewares to apply ban decisions at the edge.
- Keep the log path aligned with the NPM data volume; if NPM is relocated, update the bind mount so CrowdSec continues to receive access logs.【F:frontdoor/compose.yml†L8-L25】
- Monitor `/var/lib/crowdsec/data` for growth; rotate archives periodically to control disk usage on cache devices.
