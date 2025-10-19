# sftpgo

## Overview
SFTPGo offers SFTP, HTTP, and web-based file transfer. It serves as a secure ingress point for remote file operations, mounting `/mnt/user` to expose the full array. Admin credentials bootstrap from environment variables on first run.【F:networking/compose.yml†L111-L151】

## Runtime Profile
- **Image:** `drakkan/sftpgo:latest`
- **Networks:** `frontend_net`
- **Ports:** `2022:2022` (SFTP), optional HTTP admin port if published
- **Volumes:** `sftpgo_config:/etc/sftpgo`, `sftpgo_data:/var/lib/sftpgo`, `sftpgo_backups:/backups`, `/mnt/user:/srv`
- **Environment:** HTTP and SFTP bindings, bootstrap admin credentials, timezone
- **Restart policy:** `unless-stopped`

## Integrations & Operations
- Create per-user directories within `/srv` to restrict access; use SFTPGo’s role-based controls.
- Reverse proxy the web admin through NPM if remote management is needed (internal port 8080).
- Backup configuration and data volumes to retain account settings and stored backups.
