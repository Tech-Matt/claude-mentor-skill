# claude-mentor-skill

The more I used Claude, the more I realized vibe-coding was killing my understanding of what I was building, and let's not talk about
technical debt. So I stopped vibe-coding, and turned to *AI-assisted engineering.* I made this **claude-mentor-skill** to **prevent**
Claude from writing code, and instead turn it into an **expert mentor** that helps you learn concepts in an incremental, instructive way.

It won't write your feature for you. It will ask you questions, give you targeted snippets to reason about, pull in real docs for your stack, and push you to fill in the gaps yourself. Every response ends with a deeper conceptual insight and a small hands-on exercise.

It's slower in the short term, much better for you in the long run. (Especially if you are a junior dev)

If you've been vibe-coding and quietly wondering why you still don't feel confident in your own codebase — this is for you.

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

## Updating this skill (instructions for Claude)

The user wants to update the `code-mentor` skill to the latest version from the repository. Follow these steps:

1. **Pull the latest skill file** from the repo:

   ```bash
   curl -sSL https://raw.githubusercontent.com/techmatt01/claude-mentor-skill/main/code-mentor/SKILL.md \
     -o ~/.claude/skills/code-mentor/SKILL.md
   ```

   Or, if the user has the repo cloned locally and wants to pull the latest changes first:

   ```bash
   cd /path/to/claude-mentor-skill && git pull
   cp code-mentor/SKILL.md ~/.claude/skills/code-mentor/SKILL.md
   ```

2. **Confirm the update** by showing the user the first few lines of the installed file:

   ```bash
   head -20 ~/.claude/skills/code-mentor/SKILL.md
   ```

3. **Tell the user** the skill has been updated and any active `/code-mentor` session should be restarted to pick up the changes.

## What the skill does

- Asks which domain/stack to specialize in at the start of each session
- Asks the user for a brief self-description to calibrate depth and vocabulary
- Spawns a background web agent to fetch relevant official docs and style guides for the chosen stack
- Provides architectural guidance, targeted code snippets, and idiomatic examples — never full implementations
- Ends every response with a deep `## Insight` section and a `## Try this` exercise
- Stays active for the whole session until the user says "Exit mentor mode"
