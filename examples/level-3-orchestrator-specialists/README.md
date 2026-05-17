# Level 3: Orchestrator + Specialists

Use this level when you want one front door for delegation and synthesis.

Flow:

```text
You -> hermes-orchestrator -> /srv/agent-bus -> specialist agents
```

The orchestrator reads the Agent Control Room and routes tasks according to the registry.

The orchestrator coordinates and synthesizes. It should hand repo execution work to Codex instead of trying to run implementation loops itself.
