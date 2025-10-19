<!--
title: Networking Stack
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# Networking Stack

Networking utilities manage DNS, dynamic DNS updates, LAN monitoring, SFTP access, and bandwidth testing. Most services run in host mode or join `frontend_net`/`backend_net` depending on exposure requirements.【F:networking/compose.yml†L1-L128】

## Topology Overview
- **Networks:** `frontend_net` for public-facing HTTP services, `backend_net` for internal-only tools.
- **Volumes:** Store persistent configuration for DuckDNS, NetAlertX, AdGuard, SFTPGo, and MySpeed using named volumes or bind mounts under `/mnt/user`.【F:networking/compose.yml†L13-L117】
- **Privileges:** AdGuard runs in host mode with `NET_ADMIN` to provide DNS/DHCP; SFTPGo publishes port 2022 for SFTP access.

## Component Index

| Service | Role |
| --- | --- |
| [duckdns](duckdns.md) | Updates DuckDNS records for dynamic IP addresses. |
| [netalertx](netalertx.md) | Monitors LAN devices and triggers alerts. |
| [adguardhome](adguardhome.md) | DNS filtering and optional DHCP server. |
| [sftpgo](sftpgo.md) | SFTP/HTTP file transfer service for remote access. |
| [myspeed](myspeed.md) | Internet speed monitoring dashboard. |

### Integration Notes
- MySpeed data feeds into What’s Up Docker alerts via Discord; configure WUD triggers for bandwidth thresholds if desired.【F:devtools/compose.yml†L119-L176】
- AdGuard’s DNS should point clients to the Unraid host IP; ensure port conflicts with NPM (80/443) are avoided by using host mode.
- SFTPGo mounts `/mnt/user` for wide access—use per-user chroot directories within the application to restrict scope.
