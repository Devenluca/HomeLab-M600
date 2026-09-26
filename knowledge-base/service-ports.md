# Service Ports

| Service | Protocol | Port | Purpose |
|---|---|---:|---|
| SSH | TCP | 22 | Remote server administration |
| AdGuard DNS | TCP/UDP | 53 | DNS filtering |
| Uptime Kuma | TCP | 3001 | Monitoring dashboard |
| Samba / SMB | TCP | 445 | Network file sharing |
| AdGuard Home Web UI | TCP | 8080 | AdGuard administration |
| Stirling PDF | TCP | 8081 | Self-hosted PDF tools |
| Jellyfin | TCP | 8096 | Media server web interface |

These are the ports recorded for this lab, including its configured web UI ports.

## Access

Replace `<SERVER_LAN_IP>` with the server's LAN address. For remote access, connect through Tailscale and use `<SERVER_TAILSCALE_IP>`.

| Web interface | LAN URL |
|---|---|
| Uptime Kuma | `http://<SERVER_LAN_IP>:3001` |
| AdGuard Home | `http://<SERVER_LAN_IP>:8080` |
| Stirling PDF | `http://<SERVER_LAN_IP>:8081` |
| Jellyfin | `http://<SERVER_LAN_IP>:8096` |

See [SSH access](ssh-access.md) for administration commands.
