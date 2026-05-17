# Agent Task Bus

The task bus is a shared handoff folder for orchestrated workflows.

Suggested path on a VPS:

```text
/srv/agent-bus
```

Suggested layout:

```text
/srv/agent-bus/
  registry/
    agents.yaml
  tasks/
    seo/
      inbox/
      working/
      outbox/
      archive/
    dev/
      inbox/
      working/
      outbox/
      archive/
```

The orchestrator writes task files to specialist inboxes. Specialists write result files to outboxes. The orchestrator reads results and archives completed work.

## What Lives In The Repo

The Control Room stores the pattern:

```text
templates/task-bus/agents.yaml
templates/task-bus/task-template.md
templates/task-bus/result-template.md
templates/task-bus/handoff-template.md
```

It may also store stable registry docs for which agents exist and what they are allowed to do.

## What Stays Outside The Repo

Live task files stay in runtime:

```text
/srv/agent-bus/tasks/<role>/inbox
/srv/agent-bus/tasks/<role>/working
/srv/agent-bus/tasks/<role>/outbox
/srv/agent-bus/tasks/<role>/archive
```

Do not commit live task files if they include private user context, logs, credentials, or temporary runtime details.

## Hermes To Codex Handoffs

Use `templates/task-bus/handoff-template.md` when Hermes has clarified a task and Codex should execute it.

Good Codex handoffs include:

- objective
- repo and branch
- relevant paths
- constraints
- approval boundaries
- expected checks
- expected final output

This keeps Hermes focused on coordination and lets Codex handle implementation, debugging, tests, and repo changes.

## Task Lifecycle

```text
inbox -> working -> outbox -> archive
```

Recommended rules:

- A task in `inbox` is ready to pick up.
- A task in `working` has an owner.
- A result in `outbox` is ready for orchestrator or operator review.
- Archived tasks should keep only useful summaries and artifact links.
- Anything requiring approval should stop before the sensitive action.
