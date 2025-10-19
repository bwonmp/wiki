# landing

## Overview
Simple nginx alpine container serving the public landing page content. Static assets live in `/mnt/user/appdata/nginx/www`, and logs are written to `/mnt/user/appdata/nginx/logs`.【F:website/compose.yml†L5-L17】

## Runtime Profile
- **Image:** `nginx:alpine`
- **Networks:** `frontend_net`
- **Volumes:** `/mnt/user/appdata/nginx/www:/usr/share/nginx/html:ro`, `/mnt/user/appdata/nginx/logs:/var/log/nginx`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Typically fronted by Nginx Proxy Manager for TLS/host routing.
- Update static files directly on the host; no container rebuild required.
- Monitor log volume for disk usage and rotate as needed.
