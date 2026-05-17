# Orchestrator

The orchestrator is optional.

Add it when you want one front door for delegation and synthesis.

The orchestrator should:

- read the Agent Control Room
- know which agents exist
- know what each agent is allowed to do
- write clear task briefs
- route tasks through the task bus
- review specialist results
- synthesize the final response
- hand implementation work to Codex when repo execution is needed

The orchestrator should not:

- hold every specialist credential
- bypass specialist tools when the specialist is the source of truth
- publish, delete, rotate keys, or deploy without explicit approval
- turn into the runtime state store
- send heavy repo execution through OpenRouter when Codex can do it locally

## Good Orchestrator Work

- decide which specialist should own a task
- write clear task briefs
- split a multi-part request into bounded tasks
- compare specialist outputs
- ask for approval before risky actions
- keep the Control Room accurate after process changes

## Bad Orchestrator Work

- collecting every credential
- running every tool itself
- hiding direct specialist access
- skipping runbooks
- keeping private runtime state in the repo

## Codex Boundary

When work requires implementation, debugging, tests, or repo edits, the orchestrator should create a handoff for Codex instead of trying to execute the work through a coordination agent.

Use:

```text
templates/task-bus/handoff-template.md
```
