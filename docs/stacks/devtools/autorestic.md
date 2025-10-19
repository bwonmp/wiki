# autorestic

## Overview
Autorestic orchestrates Restic backups across your application data, pushing snapshots to an object storage backend (e.g., Backblaze B2). It mounts multiple volumes from other stacks as read-only to capture consistent backups.【F:devtools/compose.yml†L218-L238】

## Runtime Profile
- **Image:** `cupcakearmy/autorestic:latest`
- **Networks:** `backend_net`
- **Volumes:**
  - `autorestic_config:/.autorestic.yml`
  - `autorestic_cache:/root/.cache/restic`
  - Read-only mounts for Ollama, Changedetection, Wiki.js, WUD, Portnote, and `/mnt/user/appdata`
- **Environment:** `RESTIC_REPOSITORY`, `RESTIC_PASSWORD`, `B2_ACCOUNT_ID`, `B2_ACCOUNT_KEY`, timezone
- **Labels:** Provide Unraid icon metadata

## Integrations & Operations
- Ensure `.autorestic.yml` defines each target volume; update the config when adding new services to guarantee coverage.
- Validate backup success via Restic logs and consider sending notifications through Apprise or Discord.
- Keep the cache volume on SSD to speed up snapshot diffs; prune old snapshots periodically to manage storage costs.
