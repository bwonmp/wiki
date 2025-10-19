# code-server

## Overview
code-server hosts VS Code in the browser for remote development. It mounts workspace storage under `/mnt/user/appdata/code-server` and uses Authentik/Password auth for access.【F:tools/compose.yml†L122-L165】

## Runtime Profile
- **Image:** `lscr.io/linuxserver/code-server:latest`
- **Networks:** `frontend_net`
- **Volumes:** `codeserver_config:/config`, `/mnt/user/appdata/code-server:/workspace`
- **Environment:** `PASSWORD`, `PROXY_DOMAIN`, PUID/PGID, timezone
- **Healthcheck:** `curl` login page check on `127.0.0.1:8443`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Publish via NPM and secure with Authentik or built-in password.
- Map additional project directories into `/workspace` as needed.
- Backup the config volume for extensions and settings.
