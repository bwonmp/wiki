<!--
title: mariadb
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# mariadb

## Overview
MariaDB 11 supplies MySQL-compatible storage for applications such as Booklore, RomM, and other media tools that prefer MariaDB over PostgreSQL. It runs exclusively on `db_net` and exposes no host ports, reducing the attack surface.【F:databases/compose.yml†L72-L95】

## Runtime Profile
- **Image:** `mariadb:11`
- **Networks:** `db_net`
- **Volumes:** `mariadb_data:/var/lib/mysql`
- **Environment:** `MARIADB_ROOT_PASSWORD`, `MARIADB_AUTO_UPGRADE`, timezone
- **Command flags:** Tuned for ACID compliance with `--transaction-isolation=READ-COMMITTED`, `--binlog_format=ROW`, and `--innodb_flush_log_at_trx_commit=1`
- **Healthcheck:** Executes a `SELECT 1` against the root account with retries and a 25-second start period.【F:databases/compose.yml†L78-L94】

## Integrations
- Booklore references this database via JDBC using credentials stored in the Media Serving stack environment variables.【F:media_serving/compose.yml†L1-L35】
- RomM consumes the same host with the `romm_user` account; ensure privileges are scoped appropriately.【F:media_serving/compose.yml†L129-L165】
- Additional clients (e.g., CloudBeaver) can connect by joining `db_net` and authenticating with service accounts instead of root.【F:monitoring/compose.yml†L170-L215】

## Operational Notes
- Schedule regular `mysqldump` exports via Autorestic or a dedicated backup container if you need point-in-time recovery beyond volume snapshots.
- `MARIADB_AUTO_UPGRADE=1` enables automatic minor upgrades; monitor logs during image refreshes to confirm schema migrations complete without manual intervention.
