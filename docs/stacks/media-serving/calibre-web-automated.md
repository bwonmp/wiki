# calibre-web-automated

## Overview
CWA automates Calibre-Web ingest and metadata enrichment. It mounts ingest folders, Calibre libraries, and configuration to provide a streamlined pipeline for ebooks.【F:media_serving/compose.yml†L87-L135】

## Runtime Profile
- **Image:** `crocodilestick/calibre-web-automated:latest`
- **Networks:** `frontend_net`, `backend_net`
- **Ports:** `8083:8083`
- **Volumes:**
  - `/mnt/user/appdata/calibre-web-automated/:/config`
  - `/mnt/user/Downloads/completed/Books:/cwa-book-ingest`
  - `/mnt/user/Media/Books_fresh/:/calibre-library`
  - Optional plugin path mount
- **Environment:** User/Group IDs, timezone, optional Hardcover API token

## Integrations & Operations
- Shares ingest directories with Booklore; coordinate automation schedules to avoid duplicate processing.
- Consider enabling Authentik OIDC by configuring environment variables and the Authentik provider.
- Monitor download directories for cleanup—CWA removes processed files by default.
