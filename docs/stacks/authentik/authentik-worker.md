# authentik-worker

## Overview
The worker container executes Authentik’s asynchronous task queue—processing webhooks, directory sync jobs, scheduled policies, and email notifications. It mirrors the server configuration but launches with the `worker` command to connect to the same database and Redis backends.【F:authentik/compose.yml†L47-L70】

## Runtime Profile
- **Image:** `ghcr.io/goauthentik/server:2025.8.4`
- **Command:** `worker`
- **Restart policy:** `unless-stopped`
- **Networks:** `frontend_net`, `backend_net`, `db_net`
- **Health:** Inherits default healthchecks; queue liveness is monitored through Authentik’s admin UI.

## Configuration & Dependencies
- Shares `AUTHENTIK_SECRET_KEY`, PostgreSQL, and Redis credentials with the server tier to ensure job processing against the same tenant data.【F:authentik/compose.yml†L55-L70】
- Connects to the `redis` service on database index `1`, aligning with the server’s cache configuration.
- Requires access to the same `postgres` database and should be upgraded in lock-step with `authentik-server` to keep migrations synchronized.

## Operational Notes
- Scaling: multiple worker replicas can be added by deploying additional containers with the same configuration if background queues grow.
- Monitoring: check the “System” dashboard in Authentik for queue latency; prolonged delays usually indicate Redis connectivity issues or insufficient CPU.
