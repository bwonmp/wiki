# plex-hub-manager

## Overview
Automates Plex hubs and collections by calling the Plex API on a configurable schedule. Requires a Plex token and list of library names to manage.【F:media_serving/compose.yml†L206-L223】

## Runtime Profile
- **Image:** `silkychap/plex-hub-manager:latest`
- **Environment:** `PLEX_URL`, `PLEX_TOKEN`, `LIBRARY_NAMES`, `SECONDS_TO_WAIT`, `IGNORE_LIST`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Runs alongside Plex; ensure network reachability to the host’s `32400` port.
- Update the ignore list when adding curated collections so the automation doesn’t overwrite manual curation.
