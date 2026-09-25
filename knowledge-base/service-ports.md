
## `knowledge-base/service-ports.md`

```markdown
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

## Local Access

Services are accessed through the server LAN address:

```text
10.0.0.167