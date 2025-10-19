# omoide

## Overview
Omoide is an auxiliary container that performs batch operations (such as metadata cleanup) on the Immich media library. It mounts the same upload directory and a host data directory for processing artifacts.【F:immich_base/compose.yml†L71-L82】

## Runtime Profile
- **Image:** `einaeffchen/omoide`
- **Networks:** `backend_net`
- **Volumes:** `${UPLOAD_LOCATION}:/app/media`, `${HOST_DATA_DIR}:/app/data`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Use Omoide for offline maintenance tasks; it shares the same media volume as Immich so any changes are immediately reflected.
- Consider running it on-demand (by stopping/starting) to avoid consuming resources when no processing is needed.
- Adjust volume mounts if you add additional import directories; the container can map multiple subdirectories under `/app/media`.
