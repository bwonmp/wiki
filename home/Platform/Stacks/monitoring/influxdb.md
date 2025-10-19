<!--
title: influxdb
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# influxdb

## Overview
InfluxDB v2 stores time-series data such as air quality metrics and host telemetry. It mounts `influxdb_data` for persistence and exposes port `8087` for the web UI/API.【F:monitoring/compose.yml†L200-L221】

## Runtime Profile
- **Image:** `influxdb:latest`
- **Ports:** `8087:8086`
- **Networks:** `backend_net`, `monitoring_net`, `db_net`
- **Volumes:** `influxdb_data:/var/lib/influxdb2`
- **Environment:** `INFLUX_AIRQUAL_URL` and other initialization variables set via `.env`
- **Restart policy:** `always`

## Integrations & Operations
- Telegraf forwards metrics using the `INFLUX_TOKEN`; ensure the token is created and scoped appropriately.【F:monitoring/compose.yml†L222-L243】
- Scrutiny’s embedded InfluxDB is separate; consider consolidating if you want a single time-series backend.
- Backup the data directory or configure InfluxDB’s internal backup tools for retention.
