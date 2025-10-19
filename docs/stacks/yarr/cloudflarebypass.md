# cloudflare-bypass

## Overview
Companion proxy that mitigates Cloudflare challenges for CWAD and other automation services. Runs on `backend_net` with minimal configuration.【F:yarr/compose.yml†L553-L575】

## Runtime Profile
- **Image:** `ghcr.io/sarperavci/cloudflarebypassforscraping:latest`
- **Networks:** `backend_net`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Ensure dependent services reference `http://cloudflarebypassforscraping:8000` when needing bypass capabilities.
- Monitor logs for solver failures; update image as Cloudflare changes protections.
