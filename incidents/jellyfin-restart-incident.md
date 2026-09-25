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