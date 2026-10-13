# M600 Backup and Restore System

## Objective

Protect Docker application data and selected host configuration, and establish a verified configuration recovery path. A manual backup and isolated restore comparison have completed successfully. Full host rebuild/bare-metal disaster recovery and LVM rollback remain untested.

## Storage architecture

- Docker application data lives under `/srv/docker`, approximately 729 MB at inspection.
- The external media drive is mounted at `/srv/media` and is a separate physical disk from internal system storage.
- Backups live under `/srv/media/.server-backups/`: `manual/` for the manual test, `daily/` for scripted backups, and `backup.log` for backup activity.

This provides a backup on a different physical disk, but it is not yet an off-site/off-host disaster-recovery backup. Media and configuration backups share the external disk.

## Files protected

The tested manual archive included:

- `/srv/docker`
- `/etc/fstab`
- `/etc/samba/smb.conf`
- `/etc/ssh`
- `/home/darrien/.ssh/authorized_keys` (the confirmed source path)

The actual Compose files were located at:

- `/srv/docker/jellyfin/compose.yaml`
- `/srv/docker/adguard-home/compose.yaml`
- `/srv/docker/uptime-kuma/compose.yaml`
- `/srv/docker/stirling-pdf/compose.yaml`

The script backs up Docker application data and selected host configuration. Its exact implementation is not reproduced here; the supplied facts establish the explicit file list above for the manual archive.

## Files intentionally excluded

Media under `/srv/media` was intentionally excluded from the configuration archive. This workflow does not establish a media backup or a complete system image.

Backup archives may contain sensitive application data and SSH material. This repository documents paths and verification outcomes only; do not commit archives, private keys, passwords, secrets/tokens, raw sensitive databases, identifying public IPs, or unnecessary machine/user identifiers.

## Manual backup procedure and checksum verification

The completed manual test followed this sequence:

1. Temporarily stop Jellyfin, AdGuard Home, Uptime Kuma, and Stirling PDF to provide a consistent backup state.
2. Archive the protected paths listed above, excluding media, into `/srv/media/.server-backups/manual/`.
3. Restart the four Docker services; the restarts succeeded.
4. List archive contents and verify the expected Compose and host configuration files are present; they were confirmed present.
5. Generate a SHA-256 checksum and verify it; verification succeeded.

These are supplied test outcomes, not newly executed checks. No exact manual command sequence or checksum value was supplied.

## Isolated restore test

The backup was extracted into `/srv/restore-test` without overwriting production files. Restored Compose files were compared with their production copies using `diff`; the tested files matched with no differences reported.

This demonstrates that the tested archive could be extracted and that the compared configuration files matched. It does not establish successful application database recovery, production restoration, or complete bare-metal recovery.

## Automation design and retention policy

- Script: `/usr/local/sbin/m600-backup.sh`
- Oneshot service: `/etc/systemd/system/m600-backup.service`
- Timer: `/etc/systemd/system/m600-backup.timer`
- Configured nightly schedule: `02:00`, with `Persistent=true`.

The script creates timestamped archives under `/srv/media/.server-backups/daily`, stops the four Docker services before archiving, backs up Docker application data and selected host configuration, generates a SHA-256 checksum, restarts the services, and logs activity to `/srv/media/.server-backups/backup.log`. It removes daily backup files older than seven days. No manual-archive retention policy was supplied.

## Observed timestamped evidence

The supplied terminal screenshot reports server time `2026-10-13T00:49:45+00:00` (October 12 at 19:49:45 in America/Chicago). The following timestamps retain the terminal's UTC offset:

| Evidence | Observed result |
| --- | --- |
| Timer status | Loaded, enabled, and active (waiting) since `2026-10-13 00:45:24 UTC` |
| Next timer trigger | `2026-10-13 02:00:00 UTC`; the timer listing shows no last execution |
| Manual directory listing | `m600-config-2026-10-13_001541.tar` and its `.sha256` file present |
| Daily directory listing | `m600-config-2026-10-13_004158.tar` and its `.sha256` file present |
| Backup log | Starting backup at `2026-10-13T00:41:58+00:00`; backup completed at `2026-10-13T00:43:45+00:00`, naming the daily archive above |
| Container listing | All four Docker services running afterward; Jellyfin, Uptime Kuma, and Stirling PDF shown healthy |

This supports a completed scripted backup in the daily location and an enabled waiting timer. It does not establish how that run was invoked, an unattended overnight execution, daily checksum verification, or enforcement of retention. The manual checksum and isolated restore outcomes come from the supplied confirmed facts; this screenshot does not independently show those checks. The raw screenshot is not published to avoid unnecessary identifiers.

## Recovery model and limitations

Backups support recovery from data/system loss. LVM snapshots are a potential short-term rollback mechanism, not a replacement for backups.

| Recovery need | Model | Evidence / remaining work |
| --- | --- | --- |
| Configuration error | Restore configuration | Isolated extraction and Compose comparisons completed; production restore remains untested |
| Failed service | Restore service data/configuration | Data is backed up; application recovery remains untested |
| Bad system change | Future LVM rollback | Snapshot creation and rollback not tested or implemented |
| Internal disk failure | Reinstall and restore backup | Separate-disk backup exists; full host rebuild/bare-metal recovery remains future work |

Backups temporarily interrupt the four services. Checksums detect archive changes but do not prove application recovery. External-disk loss or a shared physical disaster can still lose both media and backups. Script failure handling and behavior when the external mount is absent have not been verified from supplied evidence.

## Future work

- Observe and verify an unattended scheduled backup, its checksum, and retention behavior.
- Test service data restoration and production recovery procedures.
- Test a full host rebuild/bare-metal recovery, including reinstalling and restoring the backup.
- Add an off-site/off-host backup and a separate media backup strategy.
- Evaluate short-lived pre-change LVM snapshots. The server uses volume group `ubuntu-vg`, with approximately 128.46 GB free observed; snapshot creation and rollback still require testing.
