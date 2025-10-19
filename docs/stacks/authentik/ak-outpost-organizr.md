# ak-outpost-organizr

## Overview
This outpost deploys the Authentik proxy in front of Organizr (and other UI portals) to enforce single sign-on before traffic reaches the upstream site. It runs the lightweight `ghcr.io/goauthentik/proxy` image and relies on a service account token generated from the Authentik provider configuration.【F:authentik/compose.yml†L62-L76】

## Runtime Profile
- **Image:** `ghcr.io/goauthentik/proxy:2025.8.4`
- **Command:** default entrypoint (proxy service)
- **Restart policy:** `unless-stopped`
- **Networks:** `frontend_net`
- **Volumes:** Shares `ak_media` and `ak_templates` if template overrides are needed, although none are mounted explicitly in this configuration.

## Configuration & Integrations
- `AUTHENTIK_HOST` must match the externally reachable URL of the core Authentik server so the outpost can validate tokens and refresh sessions.【F:authentik/compose.yml†L72-L77】
- `AUTHENTIK_TOKEN` is scoped to the Organizr provider; rotating the provider token requires updating this container’s environment entry.
- Since it only attaches to `frontend_net`, ensure the upstream protected service (e.g., Organizr) is reachable on the same network or via `backend_net` if dual-homed.

## Operational Notes
- Configure Nginx Proxy Manager to forward the Organizr domain to this container rather than directly to the upstream service.
- Review Authentik’s outpost deployment status after upgrades; if the proxy loses connectivity, reissue the provider token and redeploy.
