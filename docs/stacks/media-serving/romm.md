# romm

## Overview
RomM manages retro game ROMs with metadata scraping and art assets. It connects to MariaDB on `db_net` and stores assets/configuration in dedicated volumes.【F:media_serving/compose.yml†L136-L170】

## Runtime Profile
- **Image:** `rommapp/romm:latest`
- **Networks:** `frontend_net`, `db_net`
- **Volumes:** `romm_resources`, `romm_redis_data`, `romm_config`, `romm_assets`, plus `/mnt/user/Media/ROMS:/romm/library`
- **Environment:** Database host/name/user/password, `ROMM_AUTH_SECRET_KEY`, metadata provider tokens
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Ensure the `romm_user` MariaDB account exists with permissions to `romm` database.【F:databases/compose.yml†L72-L95】
- Configure metadata providers (RetroAchievements, SteamGridDB) as needed for richer art assets.
- Reverse proxy through NPM for remote access; consider Authentik SSO if multi-user.
