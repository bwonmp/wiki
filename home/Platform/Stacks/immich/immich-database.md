<!--
title: immich_postgres
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# immich_postgres

## Overview
Vector-enabled PostgreSQL instance shipping with Immich’s official image. It includes pgvector and Timescale extensions required for similarity search and metadata operations.【F:immich_base/compose.yml†L49-L70】

## Runtime Profile
- **Image:** `ghcr.io/immich-app/postgres:14-vectorchord0.4.3-pgvectors0.2.0`
- **Networks:** `backend_net`
- **Volumes:** `${DB_DATA_LOCATION}:/var/lib/postgresql/data`
- **Environment:** `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB`, `POSTGRES_INITDB_ARGS`
- **Restart policy:** `always`
- **Shared memory:** `128mb`

## Integrations & Operations
- Used exclusively by Immich; keep credentials aligned with the server container.
- Store the data directory on SSD storage to keep ingestion and ML indexing fast.
- Consider setting `DB_STORAGE_TYPE='HDD'` if you move the volume to slower disks to optimize vacuum behavior.
