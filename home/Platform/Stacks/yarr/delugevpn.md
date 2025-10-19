<!--
title: delugevpn
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# delugevpn

## Overview
DelugeVPN provides a torrent client wrapped with PIA VPN connectivity. It runs on `backend_net`, adds `NET_ADMIN`, and mounts `/dev/net/tun` for VPN tunneling.【F:yarr/compose.yml†L77-L118】

## Runtime Profile
- **Image:** `ghcr.io/binhex/arch-delugevpn:latest`
- **Networks:** `backend_net`
- **Volumes:** `/mnt/user/Downloads/torrents:/data`, `/mnt/user/appdata/delugevpn:/config`
- **Environment:** PIA credentials, VPN provider, LAN network, DNS servers, PUID/PGID
- **Devices:** `/dev/net/tun`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Ensure PIA credentials are valid; strict port forwarding and privoxy settings configured via environment.
- Coordinate download directories with Radarr/Sonarr and other automation tools.
- Monitor for VPN connectivity issues; container logs indicate handshake status.
