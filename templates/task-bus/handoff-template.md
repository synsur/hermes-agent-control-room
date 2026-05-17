---
handoff_id: HANDOFF-YYYY-MM-DD-001
created_at: YYYY-MM-DDTHH:MM:SSZ
created_by: hermes-life
execution_owner: codex
requested_by: operator
priority: normal
status: ready
requires_approval_before:
  - publishing
  - deploying
  - pushing commits
  - rotating credentials
  - destructive operations
---

# Hermes To Codex Handoff

Use this when Hermes has clarified the work and Codex should execute it.

## Objective

State the outcome Codex should produce.

## Repo / Workspace

- Repository:
- Branch:
- Relevant paths:
- Existing issue/PR:

## Context From Hermes

- Decision made:
- Priority:
- User constraints:
- Related memory or policy:

## Execution Instructions For Codex

- Inspect the existing repo first.
- Preserve existing intent and patterns.
- Make the smallest good change that solves the task.
- Run relevant tests or checks.
- Do not add raw secrets.

## Boundaries

- No deploys without approval.
- No destructive git operations without approval.
- No credential rotation without approval.
- Reference secret locations only; do not request or record secret values.

## Expected Output

- Summary of changes
- Files added or updated
- Tests/checks run
- Risks or follow-up recommendations
