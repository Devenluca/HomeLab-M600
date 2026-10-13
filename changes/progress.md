# M600 Progress Record

The setup summary consolidates project notes as of September 25, 2026. Backup evidence below reflects the separately supplied verification. This is not a live server health report.

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
- Expand monitoring and service hardening.
- Add supporting screenshots or other verification evidence.

## Discussed Future Idea

The “Digital IT Field Notes” conversation proposed an Obsidian Markdown vault, an inbox for captured notes, synchronization between the server and MacBook, and an organizer agent. The available conversation describes a design; implementation is not confirmed. It is not listed as an installed M600 service.

## Completed Backup and Restore Work

- [x] Manual configuration backup of Docker application data and selected host configuration to a separate physical disk.
- [x] Docker services restarted successfully after the manual backup.
- [x] Archive contents checked for expected Compose and host configuration files.
- [x] Manual archive SHA-256 checksum generated and verification succeeded.
- [x] Isolated restore into `/srv/restore-test`, with no production overwrite; tested restored Compose files matched production using `diff`.
- [x] Backup script, systemd oneshot service, and nightly `02:00` timer created with `Persistent=true` and a script retention policy to remove daily files older than seven days.
- [x] Supplied terminal evidence shows a completed scripted backup in the daily directory, four services running afterward, and the timer enabled and waiting.

## Remaining Backup and Recovery Work

- [ ] Verify an unattended overnight scheduled backup, daily checksum verification, and retention behavior.
- [ ] Test application/service data recovery and production configuration restoration.
- [ ] Test full host rebuild/bare-metal disaster recovery.
- [ ] Test LVM snapshot creation and rollback; LVM rollback is not implemented.
- [ ] Establish off-site/off-host disaster-recovery backups and media protection.

See [backup system evidence and limitations](backup-system.md). Current backups reside on a different physical disk, but remain attached to the same host.
