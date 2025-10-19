<!--
title: booklore
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# booklore

## Overview
Booklore serves ebooks with slick UI and optional OIDC login via Authentik. It connects to MariaDB for metadata and ingests content from multiple directories for library organization.【F:media_serving/compose.yml†L1-L34】

## Runtime Profile
- **Image:** `booklore/booklore:latest`
- **Networks:** `frontend_net`, `db_net`
- **Volumes:**
  - `/mnt/user/appdata/booklore:/app/data`
  - `/mnt/user/Media/Books_fresh:/books`
  - `/mnt/user/Downloads/completed/Books:/bookdrop`
  - `/mnt/user/Media/Calibre:/oldbooks`
- **Environment:** JDBC connection to `mariadb`, database credentials, optional OIDC parameters
- **Ports:** Exposes 6060 internally for NPM

## Integrations & Operations
- Ensure the `booklore` user exists in MariaDB with the specified password.【F:databases/compose.yml†L72-L95】
- Enable OIDC once Authentik client credentials are configured; update the `.env` to store `BOOKLORE_CLIENT_ID` and `BOOKLORE_CLIENT_SECRET`.
- Coordinate ingest directories with Calibre-Web Automated to prevent duplicate imports.
