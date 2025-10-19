# audiobookrequest

## Overview
AudiobookRequest offers a request workflow for audiobooks, backed by the shared PostgreSQL instance. It also joins `frontend_net` for reverse proxy access.【F:yarr/compose.yml†L819-L858】

## Runtime Profile
- **Image:** `markbeep/audiobookrequest:1`
- **Networks:** `db_net`, `frontend_net`
- **Volumes:** `audiobookrequest_config:/config`
- **Environment:** Postgres host/port/name/user/password, timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Ensure Postgres database `audiobookrequest` exists with user `abr` and password defined in `.env`.
- Configure base URL if publishing behind NPM to ensure correct links in notifications.
- Integrate with Readarr or manual workflows to fulfill approved requests.
