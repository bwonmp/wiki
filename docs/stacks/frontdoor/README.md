# Frontdoor Stack

The Frontdoor stack packages Nginx Proxy Manager (NPM) as the primary ingress gateway. It publishes HTTP/HTTPS on the host and orchestrates reverse-proxy routes, SSL certificates, and Authentik outpost integrations.【F:frontdoor/compose.yml†L1-L28】

## Topology Overview
- **Networks:** Attached to both `frontend_net` (public ingress) and `backend_net` (internal services).【F:frontdoor/compose.yml†L3-L20】
- **Volumes:** Stores configuration and Let’s Encrypt certificates in `npm_data` and `npm_letsencrypt` volumes; HTML landing assets mount separately from the Website stack when needed.【F:frontdoor/compose.yml†L8-L25】【F:website/compose.yml†L8-L17】
- **Ports:** Binds host ports 80/443 for HTTP/S entry.

## Component Index

| Service | Role |
| --- | --- |
| [npm](npm.md) | Nginx Proxy Manager container managing virtual hosts and certificates. |

### Integration Notes
- CrowdSec mounts the NPM log directory directly to inspect and ban malicious IPs.【F:crowdsec/compose.yml†L18-L26】
- Authentik outposts terminate authentication before forwarding to NPM-managed backends; configure SSO per host entry.
