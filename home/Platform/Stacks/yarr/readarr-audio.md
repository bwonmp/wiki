<!--
title: readarr_audio
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# readarr_audio

## Overview
Readarr (audiobook instance) manages audiobook downloads and metadata. It mounts audiobook libraries and completed downloads for ingestion.【F:yarr/compose.yml†L713-L746】

## Runtime Profile
- **Image:** `ghcr.io/pennydreadful/bookshelf:hardcover-v0.4.20.91`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/appdata/readarr:/config`, `/mnt/user/Media/Audiobooks:/audiobooks`, `/mnt/tb/Downloads/completed:/downloads`
- **Environment:** PUID, PGID, timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Coordinates with Audiobookshelf and abs-autoconverter for library updates and conversions.【F:yarr/compose.yml†L747-L810】【F:media_serving/compose.yml†L69-L157】
- Configure indexers in Prowlarr to supply audiobook feeds.
