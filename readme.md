# agent-helmsman

Opinionated skills, personas, workflows, and roles for AI agents — Claude Code, Cursor, Codex, and others.

Where `unional/skills` encodes general-purpose workflows any team can use, `agent-helmsman` is the helm: deliberate, opinionated configurations that shape how AI agents behave, communicate, and make decisions.

## Skills

| Skill | Description |
| ----- | ----------- |
| **init** | Initialize a new AGENTS.md with codebase documentation, then symlink CLAUDE.md to it. |
| **create-skill** | Create a new agent skill under `~/.agents/skills/` and symlink it into `~/.claude/skills/`. |

## Installation

```bash
# Install all skills globally
npx skills add cyberuni/agent-helmsman --all -g

# Install a specific skill
npx skills add cyberuni/agent-helmsman --skill init -g

# Install for a specific agent
npx skills add cyberuni/agent-helmsman --skill init -a claude-code -g
```
