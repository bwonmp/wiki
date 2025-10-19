# cwad

## Overview
Calibre-Web Automated Downloader UI offering manual controls over the automated ingest workflow. It runs on `frontend_net`, serves HTTP on 8481, and uses FlareSolverr for Cloudflare bypass.【F:yarr/compose.yml†L518-L552】

## Runtime Profile
- **Image:** `ghcr.io/calibrain/calibre-web-automated-book-downloader:latest`
- **Networks:** `frontend_net`
- **Ports:** `8481:8481`
- **Volumes:** `/mnt/user/Downloads/completed/Books:/cwa-book-ingest`, `fetchly_tmp:/tmp/cwa-book-downloader`
- **Environment:** Flask port, debug flag, Cloudflare bypass URL, ingest directory, API keys
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Shares ingest directory with Calibre-Web Automated; coordinate schedules to avoid conflicts.
- Protect with Authentik outpost (`ak-outpost-cwad`) if exposed externally.【F:authentik/compose.yml†L78-L82】
- Monitor `fetchly_tmp` volume for residual files and clean up if necessary.
