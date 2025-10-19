# Homelab Platform Overview

This documentation set describes the Docker-based application platform that runs on your Unraid host. Each stack folder in the repository maps to an application domain (SSO, media services, developer tooling, etc.), and every container has a dedicated reference page that captures its responsibilities, dependencies, health checks, and operational tips.

## Platform Snapshot

| Component | Details |
| --- | --- |
| Motherboard | Enginetech X11SCA-F (rev 1.01A, s/n VM205S009095) |
| BIOS | American Megatrends Inc. 2.1 (06/19/2023) |
| CPU | Intel® Core™ i7-8700K @ 3.70 GHz (HVM + IOMMU enabled) |
| Memory | 64 GiB DDR4 (maximum populated) |
| Kernel | Unraid 6.12.47 (x86_64) |
| Bonded NIC | `bond0` active-backup, MTU 1500 |
| Cache devices | WDC WDS100T2B0A SSD (1 TB), HP SSD EX900 Plus (1 TB) |
| Flash boot media | SanDisk Cruzer Fit 63.1 GB |
| Array | Fifteen-drive mix of HGST, Seagate, and Western Digital HDDs (10 TB–12 TB) |

## Docker Network Topology

The stacks share a set of pre-created Unraid bridge networks. Most services join multiple networks so that reverse proxies, application backplanes, and data services remain isolated.

- **`frontend_net`** – Public-facing applications that sit behind Nginx Proxy Manager, Authelia/Authentik outposts, or other reverse proxies.【F:frontdoor/compose.yml†L1-L25】【F:website/compose.yml†L1-L17】
- **`backend_net`** – East-west service mesh for internal APIs, utility workloads, and jobs that should not be exposed externally.【F:devtools/compose.yml†L1-L115】【F:monitoring/compose.yml†L1-L113】
- **`db_net`** – Shared database backplane hosting PostgreSQL, MariaDB, Redis, and other stateful services.【F:databases/compose.yml†L1-L95】
- **`monitoring_net`** – Telemetry overlay dedicated to observability components (Grafana, Loki, Netdata, etc.).【F:monitoring/compose.yml†L1-L203】

## Stack Index

| Stack | Summary |
| --- | --- |
| [Authentik](stacks/authentik/README.md) | Central identity provider with worker and reverse-proxy outposts.【F:authentik/compose.yml†L1-L82】 |
| [CrowdSec](stacks/crowdsec/README.md) | Log-driven intrusion detection feeding Nginx Proxy Manager bans.【F:crowdsec/compose.yml†L1-L37】 |
| [Databases](stacks/databases/README.md) | Core data services (PostgreSQL, Redis, MariaDB) consumed by nearly every stack.【F:databases/compose.yml†L11-L95】 |
| [Dev Tools](stacks/devtools/README.md) | Developer productivity platform: LLM runtime, Wiki.js, What’s Up Docker, automation, and backups.【F:devtools/compose.yml†L17-L222】 |
| [Frontdoor](stacks/frontdoor/README.md) | Edge reverse proxy via Nginx Proxy Manager.【F:frontdoor/compose.yml†L1-L28】 |
| [Immich Base](stacks/immich/README.md) | Self-hosted photo management pipeline with ML accelerator and ingest helper utilities.【F:immich_base/compose.yml†L1-L82】 |
| [Media Serving](stacks/media-serving/README.md) | Media libraries for books, video, audiobooks, ROMs, and Plex ecosystem tools.【F:media_serving/compose.yml†L1-L206】 |
| [Monitoring](stacks/monitoring/README.md) | Observability stack spanning metrics, logs, dashboards, and smart monitoring.【F:monitoring/compose.yml†L1-L203】 |
| [Networking](stacks/networking/README.md) | Edge DNS, DDNS, SFTP, and LAN telemetry utilities.【F:networking/compose.yml†L1-L128】 |
| [Tools](stacks/tools/README.md) | Knowledge management, workflow automation, file orchestration, and synchronization services.【F:tools/compose.yml†L1-L320】 |
| [Website](stacks/website/README.md) | Static landing site served via nginx alpine image.【F:website/compose.yml†L1-L17】 |
| [Yarr](stacks/yarr/README.md) | Media acquisition, request routing, and content lifecycle automation (Usenet, torrents, libraries).【F:yarr/compose.yml†L1-L200】 |

Each stack page summarizes shared volumes, network membership, credentials, and operational notes, with deep links to container-specific runbooks.
