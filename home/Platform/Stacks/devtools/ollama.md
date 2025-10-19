<!--
title: ollama
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# ollama

## Overview
Runs the Ollama runtime to host local LLM models for experimentation and integration with developer tools. Models are stored on the `ollama_models` volume so downloads persist across container updates.【F:devtools/compose.yml†L17-L45】

## Runtime Profile
- **Image:** `ollama/ollama:latest`
- **Networks:** `backend_net`
- **Volumes:** `ollama_models:/root/.ollama`
- **Healthcheck:** Polls `ollama ps` via localhost every 30 seconds with a 120-second start period, allowing GPU initialization before marking healthy.【F:devtools/compose.yml†L31-L41】
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Exposes HTTP API on port 11434 within `backend_net`; use tailscale/ssh tunnels or a reverse proxy if remote access is required.
- Autorestic mounts the model volume as read-only to back up downloaded models to object storage.【F:devtools/compose.yml†L186-L200】
- Monitor GPU utilization from Netdata or Telegraf to ensure the host has capacity for inference workloads.【F:monitoring/compose.yml†L200-L240】
