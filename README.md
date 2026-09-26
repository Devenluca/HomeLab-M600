# M600 Homelab

A hands-on Linux homelab built on a repurposed Lenovo ThinkCentre M600 to develop practical experience with Linux administration, Docker, networking, monitoring, storage, remote access, troubleshooting, and self-hosted services.

This project is designed to document not only what was built, but also how the environment is maintained, monitored, troubleshot, and improved over time.

---

## Project Goals

The primary goals of this homelab are to build practical experience relevant to:

- IT Support
- Help Desk
- Junior Systems Administration
- Linux Administration
- Cloud Infrastructure
- Networking
- Docker and containerized services
- Troubleshooting and incident response
- Technical documentation

---

## Hardware

### Server

- Lenovo ThinkCentre M600
- Intel Pentium N3700
- 4 GB DDR3L RAM
- 1 TB internal drive
- 2 TB external WD media drive

### Client Devices

- macOS laptop
- iPhone
- Smart TV / streaming devices

---

## Operating System

- Ubuntu Server 24.04 LTS
- Headless operation
- OpenSSH
- LVM storage
- Docker
- Docker Compose

The server is primarily administered remotely over SSH.

---

## Architecture

```mermaid
flowchart TD

    Internet --> Router

    Router --> LAN["Home LAN"]

    LAN --> Server["Lenovo ThinkCentre M600\nUbuntu Server"]

    Mac["macOS Admin Client"] --> LAN
    Phone["iPhone"] --> Tailscale
    Tailscale --> Server

    Server --> Docker

    Docker --> Jellyfin
    Docker --> AdGuard["AdGuard Home"]
    Docker --> Kuma["Uptime Kuma"]
    Docker --> Stirling["Stirling PDF"]

    Server --> Samba
    Server --> SSH
    Server --> Media["2 TB External Media Storage"]
```

## Documentation

- [Architecture and storage](architecture/overview.md)
- [SSH access and health checks](knowledge-base/ssh-access.md)
- [Service ports](knowledge-base/service-ports.md)
- [Jellyfin restart incident](incidents/jellyfin-restart-incident.md)
- [Work completed and next steps](changes/progress.md)

## Documented Services

Docker hosts Jellyfin, AdGuard Home, Uptime Kuma, and Stirling PDF. Samba, OpenSSH, and Tailscale run as host services. Application data is organized under `/srv/docker`; the external media drive is mounted at `/srv/media` using its filesystem UUID in `/etc/fstab`.

Uptime Kuma monitoring covers Jellyfin, AdGuard Home, SSH, Samba, and Uptime Kuma itself. SSH uses key authentication, with password authentication disabled after key access was verified.

## Project Status

This repository records the setup described in the project notes; it is not a live health report. Backups and restore testing, expanded monitoring, and further service hardening remain goals. Deployment files and screenshots have not yet been added. The Jellyfin incident still needs its root cause and resolution recorded.

Example addresses and usernames are placeholders. Substitute your own values when following the access notes.
