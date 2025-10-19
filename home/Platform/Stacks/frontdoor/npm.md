<!--
title: npm
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# npm

## Overview
Nginx Proxy Manager fronts all public services, handling reverse-proxy routing, SSL termination, and HTTP authentication layers. It resides on both `frontend_net` and `backend_net`, allowing it to reach internal services without exposing them directly to the internet.【F:frontdoor/compose.yml†L12-L25】

## Runtime Profile
- **Image:** `jc21/nginx-proxy-manager:latest`
- **Ports:** `80:80`, `443:443`
- **Networks:** `frontend_net`, `backend_net`
- **Volumes:** `npm_data:/data`, `npm_letsencrypt:/etc/letsencrypt`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- CrowdSec reads logs from `npm_data` to apply dynamic bans; ensure log format remains standard for parsers.【F:crowdsec/compose.yml†L18-L26】
- Authentik outposts typically sit in front of NPM-managed hosts; configure custom headers to forward identity assertions as required.
- Backup `npm_data` regularly to preserve host configurations and SSL certificates; Autorestic can mount the volume by referencing the named volume.
