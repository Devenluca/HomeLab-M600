# Incident: Jellyfin Unavailable After Restart

## Summary

Jellyfin became temporarily unavailable after a library scan followed by a manual restart from the Jellyfin interface.

Safari displayed:

`Safari can't connect to the server`

## Initial Concern

Possible causes included:

- Jellyfin container failure
- Docker restart failure
- Port 8096 not listening
- Application startup failure
- Network connectivity issue

## Investigation

Checked container status:

```bash
docker ps -a | grep jellyfin

cd /srv/docker/jellyfin
docker compose ps
```

## Outcome and Evidence Gaps

The original note describes the interruption as temporary, but does not include command output, the confirmed root cause, the recovery action, or a successful follow-up check. Those details remain unconfirmed. The possible causes above are hypotheses, not findings.
