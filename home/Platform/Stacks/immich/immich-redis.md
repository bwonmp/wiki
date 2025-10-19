<!--
title: immich_redis
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# immich_redis

## Overview
Dedicated Redis (Valkey) instance supporting Immich queues and caching. It runs without a password but is isolated to `backend_net` to limit exposure.【F:immich_base/compose.yml†L39-L48】

## Runtime Profile
- **Image:** `docker.io/valkey/valkey:8-bookworm`
- **Networks:** `backend_net`
- **Healthcheck:** Executes `redis-cli ping`
- **Restart policy:** `always`

## Integrations & Operations
- Used exclusively by Immich services; avoid sharing it with other stacks to keep data separation simple.
- If you enable authentication, update the server and ML container environment variables accordingly.
- Monitor memory usage—consider setting `maxmemory` in a custom config if the dataset grows beyond available RAM.
