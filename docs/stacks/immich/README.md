# Immich Stack

Immich provides self-hosted photo and video management with machine-learning assisted tagging. This stack bundles the core server, machine-learning service, Redis cache, vector-enabled Postgres database, and the Omoide utility container for bulk processing.【F:immich_base/compose.yml†L1-L82】

## Topology Overview
- **Networks:** All services run on `backend_net` to communicate with each other while remaining isolated from the public edge.【F:immich_base/compose.yml†L17-L80】
- **Storage:** Media stored under `${UPLOAD_LOCATION}` is mounted into the server and Omoide; database data resides in `${DB_DATA_LOCATION}`; models cache to `model-cache`.【F:immich_base/compose.yml†L20-L75】
- **Hardware Acceleration:** GPU/VAAPI devices are passed through via `/dev/dri` for transcoding and machine-learning inference.【F:immich_base/compose.yml†L5-L37】

## Component Index

| Service | Role |
| --- | --- |
| [immich-server](immich-server.md) | Core API/UI handling uploads, metadata, and background jobs. |
| [immich-machine-learning](immich-machine-learning.md) | Performs facial recognition and other ML tasks. |
| [immich_redis](immich-redis.md) | Redis cache supporting job queues and sessions. |
| [immich_postgres](immich-database.md) | Vector-enabled PostgreSQL storing metadata and embeddings. |
| [omoide](omoide.md) | Utility worker for batch media processing and metadata cleanup. |

### Integration Notes
- Immich uses its own dedicated Postgres container because it requires vector extensions incompatible with the shared database stack.【F:immich_base/compose.yml†L51-L70】
- Back up the `model-cache`, database, and upload directories via Autorestic or another restic job; these are not automatically captured in other stacks.
- Ensure Redis credentials remain in sync if you later secure the service with a password (current configuration does not set one, relying on network isolation).【F:immich_base/compose.yml†L39-L48】
