<!--
title: myspeed
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# myspeed

## Overview
MySpeed tracks internet speed tests over time. It stores results in `myspeed_data` and runs on `backend_net` by default.【F:networking/compose.yml†L152-L128】

## Runtime Profile
- **Image:** `germannewsmaker/myspeed:latest`
- **Networks:** `backend_net`
- **Volumes:** `myspeed_data:/myspeed`
- **Environment:** Timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Expose via NPM if you want remote access to historical speed charts.
- Consider scheduling tests during off-peak hours to avoid saturating bandwidth while streaming.
- Combine with WUD/Discord notifications for alerts when download speeds drop below thresholds.
