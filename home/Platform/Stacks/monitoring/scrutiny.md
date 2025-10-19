<!--
title: scrutiny
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# scrutiny

## Overview
Scrutiny aggregates SMART metrics for HDDs/SSDs and provides alerts on drive health. It runs privileged to access hardware and stores configuration plus embedded InfluxDB data under `/mnt/user/appdata/scrutiny`.【F:monitoring/compose.yml†L123-L158】

## Runtime Profile
- **Image:** `ghcr.io/analogj/scrutiny:master-omnibus`
- **Ports:** `8455:8080`
- **Privileges:** `SYS_RAWIO` and `SYS_ADMIN`
- **Volumes:** `/run/udev:/run/udev:ro`, `/mnt/user/appdata/scrutiny/config:/opt/scrutiny/config`, `/mnt/user/appdata/scrutiny/influxdb:/opt/scrutiny/influxdb`
- **Networks:** `db_net`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Access the UI via `http://<host>:8455`; configure notifications (email, Discord) in the web UI.
- Ensure `/run/udev` mount remains read-only to avoid interfering with host udev.
- Back up both config and InfluxDB directories for retention of historical metrics.
