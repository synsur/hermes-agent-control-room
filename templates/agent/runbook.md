# <agent-name> - Runbook

Use this for operating the agent under pressure. Commands should be copy-pasteable after replacing placeholders.

## Talk To The Agent

- Telegram:
- Slack:
- CLI:
- Dashboard:

## Quick Triage

1. Confirm the container is running.
2. Check recent logs.
3. Confirm required ports are listening.
4. Confirm runtime `.env` exists without printing values.
5. Check whether the failure is an agent issue, provider issue, or repo execution issue.

## Check Status

```bash
docker ps
docker logs <agent-name> --tail 100
ss -ltnp
test -f /srv/<agent-name>/data/.env && echo "env exists"
```

## Follow Logs

```bash
docker logs -f <agent-name>
```

## Shell Into Container

```bash
docker exec -it <agent-name> bash
```

## Restart

```bash
docker compose -f /srv/<agent-name>/docker-compose.yml restart
```

## Upgrade

```bash
docker compose -f /srv/<agent-name>/docker-compose.yml pull
docker compose -f /srv/<agent-name>/docker-compose.yml up -d
```

## Route Repo Execution To Codex

Use Codex instead of this Hermes agent for:

- code changes
- failing tests
- build errors
- dependency issues
- repo-wide refactors
- implementation from a plan

Create a handoff using `templates/task-bus/handoff-template.md` when the work needs context, constraints, and expected output.

## Rotate A Key

1. Create the new key in the provider dashboard.
2. Update `/srv/<agent-name>/data/.env`.
3. Restart the container if needed.
4. Revoke the old key.
5. Update `env-map.md`.

## Restore From Backup

See `backup.md`.

## Stop Safely

```bash
docker compose -f /srv/<agent-name>/docker-compose.yml down
```

## Escalation Notes

- If a secret was pasted into chat or committed, rotate it before continuing.
- If the agent is doing destructive work, stop and get explicit approval.
- If runtime state is corrupt, preserve a copy outside the repo before restoring.
