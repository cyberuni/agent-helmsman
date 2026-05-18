---
name: create-skill
description: Create a new agent skill under ~/.agents/skills/ and symlink it into ~/.claude/skills/ so Claude Code picks it up.
---

# Create Skill

When the user asks to create a new skill, follow this convention.

## Directory structure

Skills live in `~/.agents/skills/<name>/` and are symlinked into `~/.claude/skills/<name>`:

```
~/.agents/skills/
  <name>/
    SKILL.md        ← source of truth, edit this
~/.claude/skills/
  <name>            ← symlink → ~/.agents/skills/<name>
```

## Steps

1. Create the skill directory and file:

```bash
mkdir -p ~/.agents/skills/<name>
```

2. Write `~/.agents/skills/<name>/SKILL.md` using this template:

```markdown
---
name: <name>
description: <one-line description used to decide when to activate this skill>
---

# <Name>

<Instructions for the agent to follow when this skill is activated.>

## When to use

<Describe when this skill should be used.>

## Instructions

1. First step
2. Second step
```

3. Symlink into `.claude/skills/` so Claude Code finds it:

```bash
ln -sf ~/.agents/skills/<name> ~/.claude/skills/<name>
```

## What makes a good skill

- **Decisions over documentation.** Encode what to decide and how — don't repeat reference material the model already knows.
- **Narrow and composable.** One workflow per skill. Skills can be triggered by situation (user-facing) or called by other skills (sub-skills). Sub-skills have no situational trigger — their `description` should say "Internal skill: called by X" to avoid accidental activation. Neither type should be loaded as ambient context.
- **No baked-in opinions.** Detect the user's setup (package manager, monorepo shape, tooling) at runtime rather than assuming a specific stack.

## Notes

- `~/.agents/skills/` is the source of truth — commit or back up this directory.
- `~/.claude/skills/` only contains the symlink; never edit files there directly.
- The `description` frontmatter field is what Claude Code reads to decide when to activate the skill — make it specific and actionable. For sub-skills, prefix with "Internal skill:" to prevent unintended activation.
