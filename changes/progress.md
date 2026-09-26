# M600 Progress Record

This summary consolidates the repository's existing project notes as of September 25, 2026. It does not establish current server health.

## Documented Setup

- Repurposed Lenovo ThinkCentre M600 with Ubuntu Server 24.04 LTS, headless administration, and LVM storage.
- SSH administration from a MacBook using an Ed25519 key; password authentication disabled after key access was verified.
- Private remote access through Tailscale.
- Docker services: Jellyfin, AdGuard Home, Uptime Kuma, and Stirling PDF.
- Host services: Samba, OpenSSH, and Tailscale.
- Application data under `/srv/docker`.
- External 2 TB media storage at `/srv/media`, persisted through a filesystem UUID entry in `/etc/fstab`.
- Uptime Kuma monitoring for Jellyfin, AdGuard Home, SSH, Samba, and Uptime Kuma itself.
- Initial investigation of Jellyfin unavailability after a library scan and application restart.

## Documentation Update

- Complete Markdown formatting for the architecture diagram, SSH guide, service table, and incident commands.
- Link the existing documentation from the README.
- Use consistent placeholders for network addresses and SSH usernames.
- Distinguish documented setup from future work and unresolved incident details.

## Remaining Work

- Record the Jellyfin incident's confirmed cause, recovery action, and validation.
- Add sanitized deployment configuration files.
- Document backups and perform a restore test.
- Expand monitoring and service hardening.
- Add supporting screenshots or other verification evidence.

## Discussed Future Idea

The “Digital IT Field Notes” conversation proposed an Obsidian Markdown vault, an inbox for captured notes, synchronization between the server and MacBook, and an organizer agent. The available conversation describes a design; implementation is not confirmed. It is not listed as an installed M600 service.
