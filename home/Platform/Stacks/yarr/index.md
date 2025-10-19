<!--
title: Yarr Stack
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# Yarr Stack

The Yarr stack orchestrates media acquisition, processing, and library hygiene across Usenet, torrents, books, audiobooks, comics, and automation utilities. It spans multiple networks and integrates deeply with Plex, Radarr/Sonarr, Calibre, and other stacks.【F:yarr/compose.yml†L1-L620】

## Topology Overview
- **Networks:** Most services attach to `backend_net` for secure inter-service communication; selected apps join `frontend_net` for reverse proxying and `db_net` when database access is required (e.g., AudiobookRequest).【F:yarr/compose.yml†L1-L420】
- **Storage:** Extensive bind mounts into `/mnt/user/appdata`, `/mnt/user/Media`, and `/mnt/user/Downloads` manage configuration, completed downloads, and libraries. Named volumes preserve service-specific configuration (e.g., `huntarr_data`, `kometa_data`).
- **Security:** Some containers (DelugeVPN) run with VPN-enabled network stacks; ensure PIA credentials remain valid.

## Component Index

| Service | Role |
| --- | --- |
| [flaresolverr](flaresolverr.md) | Cloudflare bypass helper for indexers and automation. |
| [sabnzbd](sabnzbd.md) | Usenet downloader handling NZB automation. |
| [delugevpn](delugevpn.md) | Torrent client wrapped with VPN. |
| [prowlarr](prowlarr.md) | Indexer manager aggregating Usenet/torrent sources. |
| [radarr_hd](radarr_hd.md) | Radarr instance managing HD movie library. |
| [radarr_4k](radarr_4k.md) | Radarr instance managing 4K movie library. |
| [sonarr_hd](sonarr_hd.md) | Sonarr instance managing HD TV library. |
| [sonarr_4k](sonarr_4k.md) | Sonarr instance managing 4K TV library. |
| [bazarr](bazarr.md) | Subtitle management for movies/TV. |
| [overseerr](overseerr.md) | Media request portal integrated with Plex. |
| [komf](komf.md) | Manga metadata fetcher relying on FlareSolverr. |
| [mylar3](mylar3.md) | Comic downloader/manager. |
| [kapowarr](kapowarr.md) | Comic automation for metadata and downloads. |
| [pinchflat](pinchflat.md) | YouTube downloader with Plex integration. |
| [cwad](cwad.md) | Calibre-Web Automated Downloader web UI. |
| [cloudflare-bypass](cloudflarebypass.md) | Companion proxy solving Cloudflare challenges. |
| [fileflows](fileflows.md) | Media file processing and workflow engine. |
| [huntarr](huntarr.md) | Search tool bridging multiple indexers. |
| [kometa](kometa.md) | Plex metadata automation. |
| [autocaliweb](autocaliweb.md) | Calibre automation UI. |
| [readarr_audio](readarr-audio.md) | Readarr instance managing audiobooks. |
| [readarr_ebook](readarr-ebook.md) | Readarr instance managing ebooks. |
| [bookbounty](bookbounty.md) | Book request automation. |
| [audiobookrequest](audiobookrequest.md) | Audiobook request manager backed by Postgres. |
| [maintainerr](maintainerr.md) | Plex library maintenance tasks. |
| [ultimate-audiobooks](ultimate-audiobooks.md) | Toolbox container for audiobook library scripts. |
| [abs-autoconverter](abs-autoconverter.md) | Audiobook format converter tied to Audiobookshelf. |
| [titlecardmaker](titlecardmaker.md) | Plex title card generator. |

### Integration Notes
- Tautulli, Telegraf, and Grafana rely on the Radarr/Sonarr/SABnzbd API keys defined here; keep `.env` consistent across stacks.【F:monitoring/compose.yml†L222-L287】
- AudiobookRequest shares the Postgres database with other services—coordinate migrations to avoid schema conflicts.【F:yarr/compose.yml†L340-L410】【F:databases/compose.yml†L28-L49】
- Kometa, FileFlows, and Maintainerr interact directly with Plex; ensure Plex tokens remain current.
