# M600 Homelab Architecture Overview

## Purpose

This homelab was built to develop practical experience with Linux administration, Docker, networking, storage, monitoring, remote access, troubleshooting, and self-hosted services.

The environment runs on a repurposed Lenovo ThinkCentre M600 and is administered primarily from a MacBook over SSH.

## Hardware

### Server
- Lenovo ThinkCentre M600
- Intel Pentium N3700
- 4 GB DDR3L RAM
- 1 TB internal drive
- 2 TB external WD drive for media storage

### Client Devices
- MacBook
- iPhone
- Smart TV / streaming devices

## Operating System

- Ubuntu Server 24.04 LTS
- Headless operation
- OpenSSH enabled
- LVM used for internal storage

## Storage Layout

Internal storage:
- `/` for the operating system
- `/srv` for application and service data
- Docker configuration stored under `/srv/docker`

External media storage:
- Mounted at `/srv/media`
- Mounted persistently through `/etc/fstab`
- Identified by filesystem UUID
- Used primarily for Jellyfin media

## Networking

Home LAN:
- Network: `10.0.x.x`
- Gateway: `10.0.0.1`
- Server reservation: `10.x.x.x`

Remote access:
- Tailscale
- Server Tailscale IP: `100.x.x.x`

Administration:
- SSH over LAN
- SSH over Tailscale

## Docker Services

Current services include:

- Jellyfin
- AdGuard Home
- Uptime Kuma
- Stirling PDF

Additional host services include:

- Samba
- OpenSSH
- Tailscale

## Service Data

Docker applications are organized under:

`/srv/docker/<service-name>`

Persistent media storage is mounted separately at:

`/srv/media`

## Monitoring

Uptime Kuma monitors key services including:

- Jellyfin
- AdGuard Home
- SSH
- Samba
- Uptime Kuma itself

## Security

- SSH key authentication
- SSH password authentication disabled
- Tailscale used for remote private access
- No direct public exposure required for internal services
- Separate service passwords used where appropriate

## Current Goals

- Improve documentation
- Add backups and restore testing
- Expand monitoring
- Improve service hardening
- Continue building Linux and systems administration skills
