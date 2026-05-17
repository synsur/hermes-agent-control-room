# <agent-name> - Backup

## Goal

Back up durable agent state without committing secrets.

Runtime source:

```text
/srv/<agent-name>/data
```

## Include

- `SOUL.md`
- `config.yaml` with secrets removed
- `memories/`
- `skills/`
- `cron/`
- selected docs

## Exclude

- `.env`
- `auth.json`
- `sessions/`
- `logs/`
- `state.db`
- OAuth token files
- private keys

## Backup Destination

- Destination type: private git repo / object storage / snapshot / other
- Location:
- Encryption:
- Retention:
- Backup frequency:
- Restore test frequency:

## Backup Repo

- Repo:
- Visibility: private recommended
- Token scope:

## Pre-Backup Checklist

- [ ] Confirm no raw `.env` values are copied.
- [ ] Confirm OAuth token files are excluded.
- [ ] Confirm sessions and logs are excluded unless intentionally captured.
- [ ] Confirm `config.yaml` has secrets removed.
- [ ] Confirm backup token is scoped only to the backup destination.

## Restore

1. Stop the container.
2. Restore files to `/srv/<agent-name>/data`.
3. Recreate `.env` from password manager/provider dashboards.
4. Fix ownership if needed.
5. Start the container.

## Restore Commands

```bash
docker compose -f /srv/<agent-name>/docker-compose.yml down
# restore files to /srv/<agent-name>/data
chown -R root:root /srv/<agent-name>/data
docker compose -f /srv/<agent-name>/docker-compose.yml up -d
docker logs <agent-name> --tail 100
```

## Last Restore Test

- Date:
- Result:
- Notes:
