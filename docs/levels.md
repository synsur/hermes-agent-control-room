# Levels And Migration

Grow the system in levels. Do not add orchestration or automation until the manual workflow is boring and reliable.

```text
one agent -> direct specialists -> optional orchestrator -> automation
```

## Level 1: Control Room + One Agent

Use this when Hermes is still mostly one personal coordination agent.

Create:

```text
agents/hermes-life/
  inventory.md
  docker.md
  env-map.md
  runbook.md
  backup.md
```

Operating model:

- Hermes handles personal coordination, planning, review, and memory.
- Codex handles code execution when work touches repositories.
- The Control Room records how the agent runs and how to recover it.
- Runtime state stays in `/srv/hermes-life/data`, not in this repo.

Move to Level 2 when one agent has too many unrelated roles, credentials, or recurring tasks.

## Level 2: Direct Specialist Agents

Use this when roles are clear enough to separate tools, memory, credentials, and crons.

Typical specialists:

```text
hermes-life = personal coordination
hermes-seo  = SEO and content operations
hermes-dev  = development coordination, not a replacement for Codex execution
hermes-cmo  = marketing planning
hermes-ops  = VPS, backups, security checks
```

Operating model:

- You talk directly to the specialist that owns the work.
- Hermes can still help decide which specialist to use.
- Codex remains the execution layer for implementation, debugging, tests, and repo edits.
- Each specialist has its own runtime data dir and docs folder.

Move to Level 3 when choosing and coordinating specialists becomes overhead.

## Level 3: Orchestrator + Specialists

Use this when you want one front door for routing and synthesis.

Add:

```text
agents/hermes-orchestrator/
/srv/agent-bus/
```

Operating model:

- The orchestrator reads the Control Room.
- The orchestrator writes task handoffs into the task bus.
- Specialists perform bounded work and write results.
- The orchestrator reviews and synthesizes.
- You can still bypass the orchestrator and talk directly to specialists.

The orchestrator should not hold every specialist credential. It should route work to the agent or tool with the right authority.

Move to Level 4 when orchestrated tasks are repetitive and low-risk.

## Level 4: Automated Agent Team

Use this only after Levels 1-3 work manually.

Add automation for:

- backup checks
- security audits
- weekly status summaries
- stale task cleanup
- recurring SEO or ops reports
- scripted task-bus routing

Operating model:

- Automation follows the Control Room.
- Changes that publish, deploy, delete, rotate credentials, or spend money require explicit approval.
- Logs and live task state stay outside the repo.
- The Control Room records what automation exists and how to disable it.

## Migration Checklist

Before moving up a level, confirm:

- [ ] Each current agent has complete docs in `agents/<agent-name>/`.
- [ ] Runtime state is outside the repo.
- [ ] No raw secrets are committed.
- [ ] Runbooks can restart, upgrade, debug, rotate keys, and restore the agent.
- [ ] Backup scope is documented and excludes secrets.
- [ ] Codex handoffs are clear for repo execution work.
- [ ] The next level solves a real coordination problem.
