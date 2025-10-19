<!--
title: titlecardmaker
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# titlecardmaker

## Overview
TitleCardMaker generates custom Plex title cards. It mounts `/mnt/user/appdata/titlecardmaker/config` for configuration and runs on `backend_net`.【F:yarr/compose.yml†L947-L970】

## Runtime Profile
- **Image:** `ghcr.io/titlecardmaker/titlecardmaker-webui:latest`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/appdata/titlecardmaker/config:/config`
- **Environment:** timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Configure Plex token and library targets within the web UI.
- Schedule periodic runs to keep artwork in sync with new episodes.
