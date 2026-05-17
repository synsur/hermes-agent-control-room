# Level 1: Agent Control Room + One Agent

Use this level when you have one Hermes agent and want a side control plane.

Role split:

```text
Hermes = personal coordination, planning, memory, review
Codex  = repo execution when code needs to change
Control Room = durable docs and recovery notes
```

You create:

```text
agents/hermes-life/
  inventory.md
  docker.md
  env-map.md
  runbook.md
  backup.md
```

No orchestrator. No task bus. No specialist team.

Goal: one clean source of truth for the agent.

Runtime state stays outside the repo in `/srv/hermes-life/data`.
