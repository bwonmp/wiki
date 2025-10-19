# ak-outpost-cwad

## Overview
The CWAD outpost secures backend automation tools—specifically the Calibre-Web Automated Downloader—by enforcing Authentik authentication flows. It joins both `frontend_net` and `backend_net` so it can terminate inbound requests while still reaching the protected upstream container.【F:authentik/compose.yml†L78-L82】

## Runtime Profile
- **Image:** `ghcr.io/goauthentik/proxy:2025.8.4`
- **Command:** default proxy entrypoint
- **Restart policy:** `unless-stopped`
- **Networks:** `frontend_net`, `backend_net`
- **Volumes:** Shares the main Authentik media/template volumes to deliver consistent branding if applied.

## Configuration & Integrations
- `AUTHENTIK_HOST` points to the primary Authentik instance and should remain aligned with TLS certificates issued for `auth.bryanwank.com`.
- `AUTHENTIK_TOKEN` must correspond to the CWAD provider token generated in Authentik. If the provider is re-created, this value must be rotated in the compose definition or Docker secret store.【F:authentik/compose.yml†L78-L82】
- Placement on `backend_net` allows it to reach Calibre-Web Automated Downloader without exposing that service directly on the public reverse proxy.

## Operational Notes
- Deploy alongside updates to Calibre-Web Automated Downloader so the upstream service recognizes new callback URLs and headers.
- Consider enabling the optional `LISTEN` override if you need the outpost to bind a non-default port; otherwise it listens on `9000` internally and is consumed through Docker networking.
