# abs-autoconverter

## Overview
Automates audiobook format conversion for Audiobookshelf, calling its API to process new items. It runs on `backend_net` with configurable bitrate, cron schedule, and Audiobookshelf API token.【F:yarr/compose.yml†L911-L946】

## Runtime Profile
- **Image:** `cutzenfriend/abs-autoconverter:latest`
- **Networks:** `backend_net`
- **Environment:** timezone, Audiobookshelf domain, library ID, concurrency, cron schedule, bitrate, API token
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Ensure `DOMAIN` points to the Audiobookshelf service and `LIBRARY_ID` matches the target library.
- Monitor logs for conversion duration and adjust concurrency if CPU usage is high.
