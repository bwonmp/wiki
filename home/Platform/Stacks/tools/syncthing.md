<!--
title: syncthing
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# syncthing

## Overview
Syncthing synchronizes files across devices using secure, peer-to-peer replication. It mounts `/mnt/user/Media` for data sets and listens on GUI port 8384 plus sync ports 22000/21027.【F:tools/compose.yml†L409-L453】

## Runtime Profile
- **Image:** `lscr.io/linuxserver/syncthing:latest`
- **Ports:** `8384:8384`, `22000:22000/tcp`, `22000:22000/udp`, `21027:21027/udp`
- **Networks:** `frontend_net`
- **Volumes:** `syncthing_config:/config`, `/mnt/user/Media:/data1`
- **Environment:** `PUID`, `PGID`, timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Access GUI at `http://<host>:8384`; configure devices and folder shares there.
- Ensure `/data1` includes only directories you intend to sync; create subfolders for granular control.
- Combine with rclone or Autorestic to synchronize backups before offsite upload.
