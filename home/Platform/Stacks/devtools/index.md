<!--
title: Dev Tools Stack
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# Dev Tools Stack

Developer productivity and automation live here: local LLM inference with Ollama, change detection, documentation (Wiki.js), image version tracking (What’s Up Docker), secret note storage (Portnote), Restic-based backups (Autorestic), and a Discord bot for alerts.【F:devtools/compose.yml†L1-L238】

## Topology Overview
- **Networks:** Most services share `backend_net` for secure internal access; Wiki.js and Portnote also join `db_net` (and `frontend_net`) to reach PostgreSQL and to publish HTTP endpoints. The Discord bot sits on `frontend_net` to accept webhook callbacks.【F:devtools/compose.yml†L5-L237】
- **Persistent Volumes:** Each application stores state under named volumes (e.g., `ollama_models`, `changedetection_data`, `wikijs_data`, `wud_data`, `portnote_data`) or host bind mounts under `/mnt/user/appdata`. These are included in the Autorestic backup plan.【F:devtools/compose.yml†L9-L238】
- **Secrets & Tokens:** `.env` variables cover Authentik OIDC credentials, registry logins, Discord tokens, Backblaze B2 keys, and database URLs. Keep them synchronized with Authentik and Postgres configurations.

## Component Index

| Service | Role |
| --- | --- |
| [ollama](ollama.md) | Local LLM runtime exposing models over HTTP for experimentation. |
| [changedetection](changedetection.md) | Monitors website changes and triggers notifications. |
| [wikijs](wikijs.md) | Knowledge base authoring platform backed by PostgreSQL. |
| [whatsupdocker](whatsupdocker.md) | Container update watcher with Discord and Authentik integration. |
| [portnote](portnote.md) | Encrypted port inventory and credential store with Postgres backend. |
| [portnote-agent](portnote-agent.md) | Agent service that synchronizes Portnote with external sources. |
| [autorestic](autorestic.md) | Restic automation container backing up volumes to object storage. |
| [discord-wud-bot](discord-wud-bot.md) | Custom Node bot receiving WUD webhooks and relaying to Discord. |

### Integration Notes
- Portnote, Wiki.js, and Autorestic depend on the Databases stack; ensure Postgres is healthy before starting this stack.【F:databases/compose.yml†L28-L49】
- What’s Up Docker monitors image registries for all stacks; update its trigger configuration whenever you add a new repository or rename a container.【F:devtools/compose.yml†L118-L184】
- Autorestic mounts volumes from other stacks; review its config before renaming volumes or directories to avoid backup gaps.【F:devtools/compose.yml†L186-L229】
