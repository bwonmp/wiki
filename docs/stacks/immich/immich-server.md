# immich-server

## Overview
Provides the Immich API, web UI, and background job scheduler. It mounts the photo library, import directory, and configuration path, and depends on Redis plus the Immich-specific PostgreSQL database.【F:immich_base/compose.yml†L1-L48】

## Runtime Profile
- **Image:** `ghcr.io/immich-app/immich-server:${IMMICH_VERSION:-release}`
- **Command:** Default server entrypoint
- **Networks:** `backend_net`
- **Volumes:**
  - `${UPLOAD_LOCATION}:/data`
  - `/mnt/user/Media/PIctures/base:/import`
  - `/mnt/user/appdata/immich_base:/config`
  - `/etc/localtime:/etc/localtime:ro`
- **Devices:** `/dev/dri` for hardware-accelerated transcoding
- **Restart policy:** `always`

## Integrations
- Depends on `immich_redis` and `immich_postgres`; `depends_on` ensures they start before the server initializes.【F:immich_base/compose.yml†L32-L48】
- Exposed via backend network; publish through Nginx Proxy Manager or Authentik as needed for remote access.
- Shares volumes with Omoide for consistent access to media directories.

## Operational Notes
- Keep `${IMMICH_VERSION}` consistent across the server and machine-learning containers to avoid API mismatches.
- Monitor disk usage of `${UPLOAD_LOCATION}` and integrate with Autorestic backups to protect original media.
