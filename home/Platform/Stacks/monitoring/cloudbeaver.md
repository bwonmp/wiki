<!--
title: cloudbeaver
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# cloudbeaver

## Overview
CloudBeaver delivers a browser-based SQL client for managing PostgreSQL, MariaDB, and other databases running on `db_net`. It persists workspace data in `cloudbeaver_data`.【F:monitoring/compose.yml†L309-L339】

## Runtime Profile
- **Image:** `dbeaver/cloudbeaver:latest`
- **Ports:** `8948:8978`
- **Networks:** `db_net`, `backend_net`
- **Volumes:** `cloudbeaver_data:/opt/cloudbeaver/workspace`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Configure connections to Postgres (`postgres`) and MariaDB (`mariadb`) using service hostnames on `db_net`.
- Secure the admin user; CloudBeaver defaults to open registration until configured.
- Useful for schema inspection when CLI tools are unavailable.
