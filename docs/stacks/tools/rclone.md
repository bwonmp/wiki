# rclone

## Overview
Rclone manages remote storage synchronization and offers an optional RC web GUI. It mounts `/mnt/user/Media` for data access and stores configuration in `rclone_config`.【F:tools/compose.yml†L369-L408】

## Runtime Profile
- **Image:** `rclone/rclone:latest`
- **Networks:** `frontend_net`
- **Volumes:** `rclone_config:/config/rclone`, `/mnt/user/Media:/data`
- **Command:** `rcd --rc-web-gui --rc-addr :5572 --rc-user ${RCLONE_USER} --rc-pass ${RCLONE_PASS}`
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Access web GUI at `https://<host>:5572` (after proxying) with configured credentials.
- Use for cloud backups, remote mounts, or scripted tasks triggered by n8n.
- Store remote definitions in `rclone.conf` under the config volume; backup regularly.
