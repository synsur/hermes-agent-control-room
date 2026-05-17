# Security And Secrets Boundary

The Control Room documents secrets. It does not store secrets.

## Safe In This Repo

It is safe to record:

- key name
- provider
- purpose
- scope
- owner
- runtime storage location
- last rotated date
- rotation procedure
- recovery notes with secret values removed

Example:

```text
GITHUB_TOKEN
Provider: GitHub
Scope: repo read/write for shannhk/hermes-agent-control-room
Stored where: /srv/hermes-dev/data/.env
Last rotated: 2026-05-17
```

## Never Commit

Do not commit:

- API key values
- OAuth refresh tokens
- passwords
- SSH private keys
- raw `.env` files
- `auth.json`
- Google OAuth token files
- raw session directories
- runtime logs that may contain tokens
- `state.db` or other live runtime databases

The `.gitignore` blocks common secret and runtime files, but do not rely on it as the only defense.

## Runtime Secret Locations

Default runtime location:

```text
/srv/<agent-name>/data/.env
```

Container path:

```text
/opt/data/.env
```

Document the location in:

```text
agents/<agent-name>/env-map.md
```

Keep actual values in the runtime `.env`, a password manager, or the provider dashboard.

## Agent Credential Rules

- Give each agent only the credentials it needs.
- Prefer one named key per agent per provider.
- Avoid sharing one broad key across multiple agents.
- Scope keys narrowly.
- Rotate keys after role changes, suspected exposure, or accidental paste into chat.
- The orchestrator should route work, not collect every specialist credential.

## Hermes, Codex, And Provider Boundary

Hermes can coordinate sensitive work, but it should not become a vault.

Codex can execute repo changes, tests, and debugging, but task prompts should reference secret locations instead of secret values.

Avoid routing heavy execution through OpenRouter when Codex can perform the work in the repo workspace. If an external model provider is used for coordination, keep credentials scoped and avoid sending raw secrets, private tokens, or unnecessary runtime state.

## Public Exposure

Default to private:

- bind dashboards and gateway APIs to `127.0.0.1`
- expose public ports only when intentionally secured
- put public dashboards behind authentication
- record exposed ports in `agents/<agent-name>/inventory.md`

## Incident Rule

Treat any secret pasted into chat, committed to git, sent to the wrong provider, or logged publicly as compromised.

Immediate response:

1. Revoke or rotate the secret at the provider.
2. Update the runtime `.env` or secret store.
3. Restart the affected agent if needed.
4. Verify the integration works.
5. Update `agents/<agent-name>/env-map.md`.
6. Record the incident without the secret value.
