# flaresolverr

## Overview
Flaresolverr bypasses Cloudflare anti-bot protections for indexers and automation tools. It runs on `backend_net` and exposes port 8191 for HTTP requests.【F:yarr/compose.yml†L15-L40】

## Runtime Profile
- **Image:** `flaresolverr/flaresolverr:latest`
- **Networks:** `backend_net`
- **Environment:** `LOG_LEVEL`, timezone
- **Labels:** Provide Unraid icon metadata
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Komf and other metadata tools reference `http://flaresolverr:8191` for solving Cloudflare challenges.【F:yarr/compose.yml†L232-L276】
- Keep the container updated to handle evolving Cloudflare challenges.
- Monitor logs for solver errors; adjust `LOG_LEVEL` to `debug` when troubleshooting.
