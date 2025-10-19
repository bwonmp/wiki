# Databases Stack

This stack centralizes relational and cache services that back every other workload in the homelab. PostgreSQL, Redis (Valkey), and MariaDB each run on the shared `db_net` network so application stacks can discover them by container name.【F:databases/compose.yml†L1-L82】

## Topology Overview
- **Network:** `db_net` only; ingress is handled by application stacks rather than exposing ports to the host.【F:databases/compose.yml†L4-L37】
- **Persistent Volumes:** `pg_data`, `redis_data`, and `mariadb_data` keep state on cache pools for durability; Autorestic backs them up via the Dev Tools stack.【F:databases/compose.yml†L6-L37】【F:devtools/compose.yml†L186-L238】
- **Health Monitoring:** Each service defines a healthcheck to signal readiness to dependent stacks, preventing race conditions during host restarts.【F:databases/compose.yml†L28-L70】

## Component Index

| Service | Role |
| --- | --- |
| [postgres](postgres.md) | Primary PostgreSQL 16 instance hosting schemas for Authentik, Paperless, Mealie, Wiki.js, Portnote, and more. |
| [redis](redis.md) | Redis 7 cache and message broker shared by Authentik, Paperless, n8n, and other stacks. |
| [mariadb](mariadb.md) | MariaDB 11 relational database for workloads such as Booklore and RomM. |

### Integration Notes
- Keep credentials aligned with each application’s `.env` file; several services expect custom usernames (e.g., `paperless`, `mealie`, `wikijs`).【F:tools/compose.yml†L26-L178】【F:devtools/compose.yml†L83-L178】
- The optional InfluxDB service was migrated to the Monitoring stack—leave the commented block as historical reference unless you need to re-host telemetry here.【F:databases/compose.yml†L73-L95】【F:monitoring/compose.yml†L200-L239】
- If you scale Postgres or MariaDB vertically, also adjust container healthcheck thresholds and Autorestic backup schedules to account for longer start times.
