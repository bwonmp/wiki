# postgres

## Overview
Primary PostgreSQL 16 database for the environment. It stores schemas for Authentik, Wiki.js, Paperless, Mealie, n8n, Portnote, and other applications that declare credentials in their respective stacks.【F:databases/compose.yml†L28-L49】

## Runtime Profile
- **Image:** `postgres:16-alpine`
- **Networks:** `db_net`
- **Volumes:** `pg_data:/var/lib/postgresql/data`
- **Environment:** `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB`, and timezone
- **Healthcheck:** `pg_isready` executed every 10 seconds with up to 10 retries
- **Labels:** Provide Unraid metadata for icon and WebUI links

## Integrations
- Consumed by Authentik (`AUTHENTIK_POSTGRESQL__*`), Paperless (`PAPERLESS_DB*`), Mealie (`POSTGRES_*`), n8n (`DB_POSTGRESDB_*`), Wiki.js (`DB_*`), Portnote (`DATABASE_URL`), BookBounty, AudiobookRequest, and other services documented in their container pages.【F:authentik/compose.yml†L24-L60】【F:tools/compose.yml†L26-L236】【F:yarr/compose.yml†L260-L340】
- Healthcheck sequencing ensures dependent services wait until `pg_isready` passes before starting migrations.
- Consider enabling the commented `command` line to expand connection limits when more concurrent workloads are added.【F:databases/compose.yml†L40-L45】

## Operational Notes
- Place the `pg_data` volume on SSD cache for optimal performance; snapshots should be taken via Autorestic.
- Before major version upgrades, snapshot the volume and confirm compatibility of Postgres extensions (pgvector for Immich lives in a separate stack and is unaffected).
