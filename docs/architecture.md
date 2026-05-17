# Architecture

The Control Room is the source of truth for how the agent system is operated. It is a repo of docs, templates, registry files, SOPs, and recovery notes. It is not the live runtime and it is not a replacement for any agent.

The working split is:

```text
Hermes       = personal coordination brain
Codex        = execution engine for code, tests, debugging, and repo changes
Control Room = documented control plane and operating manual
Runtime      = live agent state outside the repo
```

## Responsibilities

| Layer | Owns | Does not own |
|---|---|---|
| Hermes | Planning, prioritization, memory, review, routing, personal context | Heavy implementation loops, long debug sessions, raw secret storage |
| Codex | Code changes, tests, repo edits, debugging, implementation handoffs | Personal memory, long-term operating policy, credentials beyond the current task |
| Control Room | Architecture, registry, runbooks, env maps, backup plans, handoff templates | Live sessions, logs, OAuth tokens, `.env` values, active runtime databases |
| Runtime | Agent data dirs, live config, memory files, logs, sessions, crons, secrets | Durable documentation that should survive rebuilds |

Use Hermes to decide what matters and define the work. Use Codex to execute implementation work. Use the Control Room to make the system understandable next week.

## Control Plane vs Runtime

Keep this repo clean and cloneable:

```text
/root/agent-control-room/
  README.md
  docs/
  agents/<agent-name>/
  shared/
  templates/
  examples/
  skills/
```

Keep live state outside the repo:

```text
/srv/<agent-name>/data/
  .env
  config.yaml
  SOUL.md
  memories/
  skills/
  cron/
  sessions/
  logs/
  state.db
```

The Control Room may describe where runtime files live. It must not contain the live secret values or volatile state.

## Agent Docs Layout

Each agent gets one folder named with its stable slug:

```text
agents/hermes-life/
  inventory.md
  docker.md
  env-map.md
  runbook.md
  backup.md
```

Optional specialist examples:

```text
agents/hermes-seo/
agents/hermes-dev/
agents/hermes-cmo/
agents/hermes-ops/
agents/hermes-orchestrator/
```

Use `docs/naming.md` to keep container names, data dirs, bot names, key names, and doc paths aligned.

## Access Paths

You are not locked into one path.

```text
Control path:
  You -> Control Room
  Use for architecture, registry updates, runbooks, backups, security notes.

Coordination path:
  You -> Hermes
  Use for planning, prioritization, memory, review, and deciding who should do what.

Execution path:
  You or Hermes -> Codex
  Use for implementation, debugging, tests, repo edits, and PR-ready changes.

Direct specialist path:
  You -> hermes-seo / hermes-dev / hermes-cmo / hermes-ops
  Use when you already know which specialist owns the work.

Orchestrated path:
  You -> hermes-orchestrator -> Task Bus -> Specialist -> Orchestrator -> You
  Use when a task needs routing, parallel specialist work, or synthesis.
```

## Execution Boundary

Prefer Codex for heavy execution work where possible:

- repository edits
- implementation plans that must become code
- debugging loops
- test runs
- dependency and build failures
- file-by-file refactors

Avoid sending heavy execution loops through OpenRouter when Codex can do the work locally or through the repo workspace. Hermes can still coordinate the work and review the result.

## Recommended Container Pattern

Use one Docker container per long-running Hermes agent.

Each agent gets:

- its own `/srv/<agent-name>/data`
- its own container-mounted `/opt/data`
- its own `.env`
- its own memory, skills, sessions, crons, and logs
- its own messaging tokens
- its own backup plan
- its own Control Room docs folder

Do not run two gateway processes against the same data directory.

## Task Bus Pattern

The task bus is optional. Add it when direct messages stop scaling.

```text
/srv/agent-bus/
  registry/agents.yaml
  tasks/<role>/inbox/
  tasks/<role>/working/
  tasks/<role>/outbox/
  tasks/<role>/archive/
```

The orchestrator writes task files. Specialists write result files. The Control Room stores the templates and registry shape, while the live task files stay in `/srv/agent-bus`.
