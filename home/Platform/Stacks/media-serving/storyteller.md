<!--
title: storyteller
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# storyteller

## Overview
Storyteller is a self-hosted audiobook and ebook streaming platform with GPU acceleration. It mounts libraries for books and audiobooks and uses `/mnt/user/appdata/storyteller` for persistent data.【F:media_serving/compose.yml†L230-L266】

## Runtime Profile
- **Image:** `registry.gitlab.com/storyteller-platform/storyteller:latest`
- **Networks:** `frontend_net`
- **Volumes:** `/mnt/user/appdata/storyteller:/data`, `/mnt/user/Media/Books_fresh:/booklibrary`, `/mnt/user/Media/Audiobooks:/audiolibrary`
- **Devices:** `/dev/dri`
- **Ports:** `8431:8001`
- **Resources:** CPU/memory limits (2 CPUs, 24 GB) with reservations

## Integrations & Operations
- Align library directories with Audiobookshelf and Booklore to prevent duplicates.
- Ensure GPU drivers support the container’s acceleration requirements.
- Monitor resource consumption; adjust Docker resource limits if workloads expand.
