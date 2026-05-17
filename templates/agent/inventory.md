# <agent-name> - Inventory

Use this file as the top-level record for one agent. Keep it accurate enough that a new operator can identify the agent, find its runtime, understand its authority, and know when to use it.

## Role

- Primary role:
- Short description:
- Level: 1 one-agent / 2 direct specialist / 3 orchestrated specialist / 4 automated
- Coordination owner: Hermes / operator / orchestrator
- Execution boundary: use Codex for repo changes, debugging, tests, and implementation work

## Where It Runs

- Host:
- Deployment style: Docker container / root install / other
- Container name:
- Image:
- Host data dir:
- Container data dir: `/opt/data`
- Compose file:
- Control Room docs dir: `agents/<agent-name>/`

## Ports

| Host port | Container port | Purpose | Exposure |
|---|---:|---|---|
| TBD | 8642 | Gateway/API | localhost/private/public |
| TBD | 9119 | Dashboard | localhost/private/public |

Record public exposure deliberately. Prefer `127.0.0.1` unless a dashboard or API is protected.

## Messaging Integrations

- Telegram:
- Slack:
- Discord:
- Other:

## Credentials

See `env-map.md`. Do not paste values here.

## Memory & Skills

- Memory:
- Skills:
- Crons:
- Sessions:

## Allowed Work

- 

## Forbidden Work

- publishing without approval
- deploys without approval
- destructive operations without approval
- credential rotation without approval
- storing raw secrets in the Control Room

## When To Use This Agent

- 

## When To Use Hermes Instead

- planning
- prioritization
- personal memory
- final review
- deciding which agent or tool should own work

## When To Use Codex Instead

- implementation
- debugging
- tests
- repo edits
- dependency or build failures
- PR-ready changes

## Owner

- 

## Last Reviewed

- Date:
- Reviewed by:
