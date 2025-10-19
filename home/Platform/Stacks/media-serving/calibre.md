<!--
title: calibre
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# calibre

## Overview
LinuxServer’s Calibre container provides a full desktop GUI via noVNC for managing ebook libraries, conversions, and metadata editing. It mounts multiple host directories for books and downloads.【F:media_serving/compose.yml†L49-L86】

## Runtime Profile
- **Image:** `lscr.io/linuxserver/calibre`
- **Networks:** `backend_net`
- **Ports:** `8781:8080`
- **Volumes:**
  - `/mnt/user/Media/Books_fresh/:/calibre_books`
  - `/mnt/user/Downloads/:/calibre_downloads`
  - `/mnt/user/Media/Books:/old_books`
- **Environment:** `PUID=99`, `PGID=100`, timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Use alongside Calibre-Web Automated; coordinate ingest directories to avoid conflicts.
- Keep `PUID/PGID` aligned with Unraid’s `nobody` account so generated files remain accessible to other containers.
- Secure the noVNC interface via Nginx Proxy Manager or Authentik if exposed beyond the LAN.
