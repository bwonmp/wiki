# Website Stack

Serves the public landing page via a minimal nginx alpine container mounted with static HTML content. Works in tandem with Nginx Proxy Manager for TLS termination.【F:website/compose.yml†L1-L17】

## Component Index

| Service | Role |
| --- | --- |
| [landing](landing.md) | Static site served from `/mnt/user/appdata/nginx/www`. |

### Integration Notes
- Update content under `/mnt/user/appdata/nginx/www`; changes are picked up instantly by the container.
- Access logs live under `/mnt/user/appdata/nginx/logs`, useful for analytics or troubleshooting.
