<!--
title: bentopdf
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# bentopdf

## Overview
BentoPDF converts documents to PDF using containerized tooling. It mounts configuration from `/mnt/user/appdata/bentopdf` and drops most Linux capabilities for hardened execution.【F:tools/compose.yml†L454-L489】

## Runtime Profile
- **Image:** `bentopdf/bentopdf:latest`
- **Networks:** `frontend_net`
- **Volumes:** `/mnt/user/appdata/bentopdf:/config`
- **Security:** Drops all capabilities except `CHOWN`, `SETGID`, `SETUID`; `no-new-privileges` enabled
- **Environment:** `PUID`, `PGID`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Expose via NPM if users need web access; ensure Authentik protects the endpoint.
- Store conversion outputs within the bind-mounted config directory or pass-through volumes as needed.
- Monitor container logs for conversion errors; update image when new format support is added.
