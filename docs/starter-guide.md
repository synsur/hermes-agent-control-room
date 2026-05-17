# Starter Guide

Use this repo as the operating manual for your agent system.

The default workflow is:

```text
Hermes decides and remembers.
Codex executes code work.
The Control Room records how the system is supposed to run.
Runtime state stays outside the repo.
```

## 1. Clone The Control Room

On the VPS or workstation that will hold the docs:

```bash
git clone https://github.com/shannhk/hermes-agent-control-room.git /root/agent-control-room
cd /root/agent-control-room
```

If you are starting from a fresh VPS, use the bundled `create-vps` and `setup-control-room` skills to provision the server and install the basic tools.

## 2. Read The Core Docs

Read these first:

```text
docs/architecture.md
docs/levels.md
docs/security.md
docs/naming.md
```

Keep this rule in mind:

```text
/root/agent-control-room = docs, templates, registry, recovery notes
/srv/<agent-name>/data = live runtime state and secrets
```

## 3. Register Your First Hermes Agent

Start with one personal coordination agent, usually `hermes-life`.

```bash
mkdir -p agents/hermes-life
cp templates/agent/*.md agents/hermes-life/
```

Fill in:

```text
agents/hermes-life/inventory.md
agents/hermes-life/docker.md
agents/hermes-life/env-map.md
agents/hermes-life/runbook.md
agents/hermes-life/backup.md
```

Do not paste raw secrets into any of these files. Record secret names, scopes, providers, and runtime locations only.

## 4. Use The Daily Operating Loop

For planning and priorities:

```text
Ask Hermes.
```

For implementation, debugging, tests, and repo edits:

```text
Hand the task to Codex with a clear brief.
Use templates/task-bus/handoff-template.md when useful.
```

For durable system updates:

```text
Update the Control Room docs.
```

For live state, logs, sessions, or `.env` values:

```text
Use /srv/<agent-name>/data or the relevant runtime system.
Do not copy live state into the repo.
```

## 5. Add Specialists Only When Needed

Add direct specialists when the role needs separate memory, tools, credentials, ports, or crons.

Common names:

```text
hermes-seo
hermes-dev
hermes-cmo
hermes-ops
```

Each specialist gets its own:

- docs folder in `agents/<agent-name>/`
- runtime data dir in `/srv/<agent-name>/data`
- `.env`
- ports
- backup plan
- allowed and forbidden work list

## 6. Add An Orchestrator Later

Add `hermes-orchestrator` only when one front door would reduce overhead.

The orchestrator should:

- read the Control Room
- route work through the task bus
- synthesize results
- ask for approval before sensitive operations

The orchestrator should not become the one agent with every credential.

## 7. Automate Last

Automate only after manual delegation works.

Good early automations:

- backup checks
- security checklist reminders
- weekly summaries
- stale task cleanup

Require explicit approval for:

- deploys
- destructive operations
- credential rotation
- public publishing
- spending money

## First Milestone

You are ready to move beyond Level 1 when:

- [ ] One Hermes agent is documented in `agents/<agent-name>/`.
- [ ] You can restart and debug it from `runbook.md`.
- [ ] `env-map.md` records secret locations without values.
- [ ] `backup.md` explains what to include and exclude.
- [ ] Codex handoffs are clear for repo execution work.
- [ ] `git status` shows no accidental runtime files or secrets.
