<!--
title: discord-wud-bot
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# discord-wud-bot

## Overview
Custom Node.js bot that receives HTTP callbacks from What’s Up Docker and posts update notifications into a Discord channel. Source code lives on the host under `/mnt/user/appdata/discord-wud-bot` so you can iterate on the bot without rebuilding the container.【F:devtools/compose.yml†L229-L238】

## Runtime Profile
- **Image:** `node:18-alpine`
- **Command:** `node index.js`
- **Networks:** `frontend_net`
- **Ports:** `8085:8080` exposes the webhook endpoint to WUD
- **Volumes:** `/mnt/user/appdata/discord-wud-bot:/usr/src/app`
- **Environment:** Discord bot token, channel ID, WUD API endpoint, and port

## Integrations & Operations
- The WUD container posts updates to `http://discord-wud-bot:8080/wud/update`; keep network connectivity open between the two services.【F:devtools/compose.yml†L152-L167】
- Store bot secrets in `.env` and rotate them when regenerating Discord tokens.
- Use PM2 or nodemon locally (via the bind mount) if you want hot reload without container restarts.
