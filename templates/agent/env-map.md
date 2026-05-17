# <agent-name> - Env / Secret Map

This file records where secrets live, not their values.

Do not paste raw `.env` contents here.

## Container `.env`

- Inside container: `/opt/data/.env`
- On host: `/srv/<agent-name>/data/.env`
- Owner:
- Rotation owner:

## Keys

| Env var | Purpose | Provider | Scope | Stored where | Last rotated | Notes |
|---|---|---|---|---|---|---|
| `EXAMPLE_API_KEY` | Example | Example | Read-only | `/srv/<agent-name>/data/.env` | TBD | Example only |

## Non-Secret Config

| Name | Purpose | Value or location | Notes |
|---|---|---|---|
| `PORT` | Gateway/API port | TBD | Not secret |

## Provider Dashboards

| Provider | Dashboard URL | Key name in provider | Owner |
|---|---|---|---|
| Example | `https://example.com` | `<agent-name>:example` | TBD |

## Rules

- Do not paste raw secret values in this file.
- Use per-agent key names in provider dashboards.
- Prefer least privilege.
- Rotate any key pasted into chat.
- Keep orchestrator credentials narrow; route specialist work to the specialist instead of sharing broad keys.

## Rotation Procedure

1. Create the replacement key in the provider dashboard.
2. Put the value in the runtime secret location.
3. Restart the agent if required.
4. Verify the integration.
5. Revoke the old key.
6. Update the `Last rotated` column above.
