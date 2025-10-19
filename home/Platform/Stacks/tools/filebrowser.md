<!--
title: filebrowser
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# filebrowser

## Overview
FileBrowser exposes a web UI to browse, upload, and edit files across `/mnt/user`. It uses an external configuration volume (`tools_new_filebrowser_config`) to preserve state across stack reorganizations.【F:tools/compose.yml†L166-L205】

## Runtime Profile
- **Image:** `filebrowser/filebrowser:latest`
- **Networks:** `backend_net`
- **Ports:** `8284:80`
- **Volumes:** `tools_new_filebrowser_config:/config`, `/mnt/user:/srv:rw`, `/var/lib/docker/volumes/:/srv/docker:rw`
- **Command:** `--database /config/filebrowser.db --address 0.0.0.0 --port 80`
- **Healthcheck:** `wget http://localhost`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Reverse proxy through NPM and secure with Authentik or built-in user management.
- Ensure proper ACLs within FileBrowser to prevent accidental modification of critical volumes.
- Autorestic backs up the configuration volume to preserve user accounts and settings.【F:devtools/compose.yml†L186-L200】
