<!--
title: kapowarr
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# kapowarr

## Overview
Kapowarr automates comic metadata and downloads, complementing Mylar. It mounts appdata, download staging, and comic libraries for ingestion.【F:yarr/compose.yml†L450-L484】

## Runtime Profile
- **Image:** `mrcas/kapowarr:latest`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/appdata/kapowarr:/config`, `/mnt/user/Downloads/completed/comics:/app/temp_downloads`, `/mnt/user/Media/Comics:/content`
- **Environment:** timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Configure download clients and metadata providers via UI.
- Ensure directories align with Mylar and Komga to avoid duplicate storage.
