# Agents

This folder is the Control Room registry for agent-specific docs.

Create one folder per agent using the stable agent slug:

```text
agents/hermes-life/
agents/hermes-seo/
agents/hermes-dev/
agents/hermes-cmo/
agents/hermes-ops/
agents/hermes-orchestrator/
```

Each agent folder should contain:

```text
inventory.md
docker.md
env-map.md
runbook.md
backup.md
```

For orchestrated setups, use `templates/task-bus/agents.yaml` as the machine-readable registry shape. Keep the per-agent markdown files as the operator-readable source of truth.

Use:

```bash
mkdir -p agents/<agent-name>
cp templates/agent/*.md agents/<agent-name>/
```

Rules:

- Keep agent docs in this repo.
- Keep live runtime state in `/srv/<agent-name>/data`.
- Keep live task-bus files in `/srv/agent-bus`.
- Do not commit raw secrets.
- Use Hermes for coordination and Codex for repo execution work.
