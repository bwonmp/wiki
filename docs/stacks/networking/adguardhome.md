# adguardhome

## Overview
AdGuard Home delivers DNS filtering and optional DHCP services. It runs in host network mode to bind port 53/udp+tcp and includes persistent configuration/work directories.【F:networking/compose.yml†L85-L110】

## Runtime Profile
- **Image:** `adguard/adguardhome:latest`
- **Network mode:** `host`
- **Capabilities:** `NET_ADMIN`
- **Volumes:** `adguard_conf:/opt/adguardhome/conf`, `adguard_work:/opt/adguardhome/work`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Initial setup via `http://<host>:3000`; change the admin port after configuration to avoid conflicts with NPM.
- Configure upstream DNS and custom blocklists to suit home network policies.
- If running DHCP, ensure no other DHCP server is active on the LAN.
