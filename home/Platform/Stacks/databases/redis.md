<!--
title: redis
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# redis

## Overview
Redis 7 (Valkey) provides caching, session storage, and queue backends for Authentik, Paperless, n8n, and other services. It operates on the `db_net` network so consumers can reference it by the `redis` hostname.【F:databases/compose.yml†L52-L70】

## Runtime Profile
- **Image:** `redis:7-alpine`
- **Command:** `redis-server --appendonly yes --requirepass ${REDIS_PASSWORD}`
- **Networks:** `db_net`
- **Volumes:** `redis_data:/data`
- **Environment:** `TZ`, `REDIS_PASSWORD`
- **Healthcheck:** Executes `redis-cli ping` with password authentication every 10 seconds; allows a 20-second start period.【F:databases/compose.yml†L59-L68】

## Integrations
- Authentik uses database index `1` for authentication sessions and background job state.【F:authentik/compose.yml†L33-L70】
- Paperless and n8n reference additional database indexes (`2` and `3` respectively) to segregate keys.【F:tools/compose.yml†L26-L236】
- Monitoring tools (e.g., Autorestic or external dashboards) can connect over `db_net`; avoid exposing ports publicly.

## Operational Notes
- Keep `REDIS_PASSWORD` synchronized with all consuming containers; mismatched credentials are a common startup failure.
- Monitor AOF growth in `/data`; periodic restarts or the `BGREWRITEAOF` command will compact logs.
- If you add TLS termination, consider fronting Redis with stunnel or migrating to a managed service; Unraid host network remains local-only.
