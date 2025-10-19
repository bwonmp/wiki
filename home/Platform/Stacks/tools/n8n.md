<!--
title: n8n
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# n8n

## Overview
n8n automates workflows and integrates with APIs. It relies on Postgres for persistence, Redis (DB 3) for queues, and exposes webhooks at `https://n8n.bryanwank.com`.【F:tools/compose.yml†L313-L368】

## Runtime Profile
- **Image:** `docker.n8n.io/n8nio/n8n:latest`
- **Networks:** `frontend_net`, `db_net`
- **Volumes:** `n8n_data:/home/node/.n8n`
- **Environment:** Postgres credentials, encryption key, Redis queue config, webhook URL, timezone
- **Healthcheck:** simple Node exit status check
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Keep `N8N_ENCRYPTION_KEY` secret; changing it invalidates saved credentials.
- Ensure Redis DB index `3` is available; other services use DB 1 (Authentik) and DB 2 (Paperless).
- Configure Authentik or NPM to secure the web UI and webhook endpoints.
