<!--
title: mealie
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# mealie

## Overview
Mealie manages recipes with meal planning, shopping lists, and Authentik-backed login. It relies on PostgreSQL for data storage and listens on internal port 9000 (proxied externally).【F:tools/compose.yml†L206-L245】

## Runtime Profile
- **Image:** `ghcr.io/mealie-recipes/mealie:latest`
- **Networks:** `frontend_net`, `db_net`
- **Volumes:** `mealie_data:/app/data`
- **Environment:** Database configuration, OIDC settings, timezone, `MEALIE_OPTS` forwarding header allowance
- **Command:** `uvicorn mealie.app:app --host 0.0.0.0 --port 9000 --forwarded-allow-ips="*"`
- **Healthcheck:** `true`

## Integrations & Operations
- Configure Authentik provider with redirect URIs to `https://recipes.bryanwank.com`.
- Ensure Postgres `mealie` user/password exist in the Databases stack.【F:databases/compose.yml†L28-L49】
- Backup `mealie_data` for recipe exports and attachments.
