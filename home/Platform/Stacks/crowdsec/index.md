<!--
title: CrowdSec Stack
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# CrowdSec Stack

CrowdSec inspects reverse-proxy logs to detect malicious traffic patterns and feed remediation decisions back into the edge. The stack is intentionally slim—just the CrowdSec agent—with optional bouncer services commented out when not required.【F:crowdsec/compose.yml†L1-L37】

## Topology Overview
- **Networks:** Connects to `backend_net` so it can talk to Nginx Proxy Manager (NPM) and expose its local API to bouncers.【F:crowdsec/compose.yml†L3-L23】
- **Log Source:** Mounts the NPM log directory directly from the Docker volume, allowing CrowdSec parsers to inspect HTTP access attempts in near real time.【F:crowdsec/compose.yml†L18-L24】
- **Data Persistence:** Stores configuration under `/etc/crowdsec/config` and historical decisions under `/crowdsec/data` so bans survive restarts.【F:crowdsec/compose.yml†L24-L27】

## Component Index

| Service | Role |
| --- | --- |
| [crowdsec](crowdsec.md) | Behavioral analysis engine ingesting NPM logs and publishing ban decisions over the local API. |

### Integration Notes
- If you enable the optional nginx bouncer, remember to rejoin it to `frontend_net` so it can talk to NPM over the management API while authenticating with `CROWDSEC_LAPI_KEY`.
- What’s Up Docker in the Dev Tools stack can monitor the `crowdsec` image tag for updates and alert via Discord when new detection rules ship.【F:devtools/compose.yml†L125-L176】
