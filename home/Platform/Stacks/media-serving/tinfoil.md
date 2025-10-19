<!--
title: tinfoil-hat
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# tinfoil-hat

## Overview
Tinfoil Hat hosts a Nintendo Switch NSP repository with authentication, optional messaging, and save synchronization support.【F:media_serving/compose.yml†L207-L250】

## Runtime Profile
- **Image:** `vinicioslc/tinfoil-hat:latest`
- **Networks:** `frontend_net`
- **Volumes:** `/mnt/user/Media/Games/Switch/:/games/`
- **Environment:** Authentication users, welcome/unauthorized messages, save sync configuration
- **Ports:** SFTP/FTP-related via `NX_PORTS`

## Integrations & Operations
- Manage users via the `AUTH_USERS` environment variable (format `user:pass`).
- Expose via Authentik or restrict to LAN due to game distribution nature.
- Regularly update NSP library and ensure disk usage remains within array capacity.
