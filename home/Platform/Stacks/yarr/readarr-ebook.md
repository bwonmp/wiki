<!--
title: readarr_ebook
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# readarr_ebook

## Overview
Readarr ebook instance handles ebook downloads and metadata. Shares architecture with the audio instance but targets `/mnt/user/Media/Books_fresh` for library storage and exposes port 8788.【F:yarr/compose.yml†L747-L790】

## Runtime Profile
- **Image:** `ghcr.io/pennydreadful/bookshelf:hardcover-v0.4.20.91`
- **Networks:** `backend_net`
- **Ports:** `8788:8787`
- **Volumes:** `/mnt/user/appdata/readarr_ebook:/config`, `/mnt/user/Media/Books_fresh:/ebooks`, `/mnt/tb/Downloads/completed:/downloads`
- **Environment:** PUID, PGID, timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Combine with BookBounty and CWAD for ingest automation.
- Configure metadata providers and quality profiles as needed for ebooks.
