<!--
title: portnote-agent
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# portnote-agent

## Overview
The Portnote agent synchronizes data from the application to external integrations. It runs alongside the main Portnote API and connects directly to PostgreSQL using service credentials.【F:devtools/compose.yml†L210-L217】

## Runtime Profile
- **Image:** `haedlessdev/portnote-agent:latest`
- **Networks:** `db_net`
- **Environment:** `DATABASE_URL` with root credentials and host `postgres`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Ensure the database URL stays in sync with the credentials used by the main Portnote container; mismatches will cause authentication failures.
- Consider rotating credentials to a dedicated Postgres role with limited privileges if the agent does not require superuser access.
