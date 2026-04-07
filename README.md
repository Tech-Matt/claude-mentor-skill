# claude-mentor-skill

Are you tired of not being able to understand your whole codebase? It's simple, stop vibe-coding and start learning. The **claude-mentor-skill** is

## Installing this skill (instructions for Claude)

The user wants to install the `code-mentor` skill from this repository. Follow these steps:

1. **Copy the skill file** from this repo into the user's Claude skills directory:

   ```bash
   mkdir -p ~/.claude/skills/code-mentor
   curl -sSL https://raw.githubusercontent.com/techmatt01/claude-mentor-skill/main/code-mentor/SKILL.md \
     -o ~/.claude/skills/code-mentor/SKILL.md
   ```

   Or, if the user has already cloned the repo locally, copy it directly:

   ```bash
   mkdir -p ~/.claude/skills/code-mentor
   cp /path/to/claude-mentor-skill/code-mentor/SKILL.md ~/.claude/skills/code-mentor/SKILL.md
   ```

2. **Confirm the file is in place:**

   ```bash
   cat ~/.claude/skills/code-mentor/SKILL.md
   ```

3. **Tell the user** the skill is installed and can be activated by typing `/code-mentor` in any Claude Code session.

> If the user's Claude skills directory is somewhere other than `~/.claude/skills/`, check `~/.claude/settings.json` or ask the user where their skills are stored.

## What the skill does

- Asks which domain/stack to specialize in at the start of each session
- Asks the user for a brief self-description to calibrate depth and vocabulary
- Spawns a background web agent to fetch relevant official docs and style guides for the chosen stack
- Provides architectural guidance, targeted code snippets, and idiomatic examples — never full implementations
- Ends every response with a deep `## Insight` section and a `## Try this` exercise
- Stays active for the whole session until the user says "Exit mentor mode"
