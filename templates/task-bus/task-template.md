---
task_id: TASK-YYYY-MM-DD-001
created_at: YYYY-MM-DDTHH:MM:SSZ
created_by: hermes-orchestrator
assigned_to: hermes-seo
requested_by: user
priority: normal
status: ready
requires_approval_before:
  - publishing
  - pushing commits
  - rotating credentials
  - destructive operations
---

# Task Handoff

Use this when an orchestrator or operator hands bounded work to a specialist.

## Task

Describe the task in one or two sentences.

## Context

Add relevant context and paths.

## Source Of Truth

- Control Room docs:
- Runtime path if needed:
- Repo path if needed:
- Related issue/PR:

## Execution Boundary

- Use Hermes for coordination, memory, prioritization, and review.
- Use Codex for code changes, debugging, tests, and repo edits.
- Do not route heavy implementation loops through OpenRouter when Codex can execute locally.

## Constraints

- Do not expose secrets.
- Do not perform destructive operations without approval.
- Do not publish, deploy, rotate credentials, or spend money without approval.

## Expected Output

- Findings
- Files changed or artifacts created
- Risks and assumptions
- Recommended next action
