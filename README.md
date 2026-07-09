# ChromieCraft Agent Toolkit

Shared agent skills and tooling for ChromieCraft workflows.

## Skills

- `skills/triaging` - ChromieCraft bug triage assistant skill, imported from the triage-skill work in `chromiecraft/chromiecraft`.
- `skills/skill-feedback-pr-flow` - Skill feedback workflow that routes durable improvements through self-improve, Syncwheel PR delivery, and explicit install timing.

## AgentWheel

This repository includes `agentwheel.json`, so it can be added as an AgentWheel package:

```bash
agentwheel add github:chromiecraft/chromiecraft-agent-toolkit --adapter openclaw
agentwheel update --dry-run
agentwheel update
```

## Notes

This repository is intentionally small for now. Add more artifact folders, such as `instructions/`, `rules/`, `commands/`, `mcp/`, or `hooks/`, only when they are actually needed.
