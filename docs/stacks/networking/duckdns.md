# duckdns

## Overview
DuckDNS updates dynamic DNS records for one or more subdomains using LinuxServer’s container. It stores configuration under `duckdns_config` and authenticates with the DuckDNS token from `.env`.【F:networking/compose.yml†L23-L47】

## Runtime Profile
- **Image:** `lscr.io/linuxserver/duckdns:latest`
- **Networks:** `frontend_net`
- **Volumes:** `duckdns_config:/config`
- **Environment:** `SUBDOMAINS`, `TOKEN`, timezone, PUID/PGID
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Configure Cron updates via the container’s config if custom intervals are required.
- Ensure subdomain list matches records configured in DuckDNS dashboard.
- Monitor logs for update failures (e.g., connectivity or token issues).
