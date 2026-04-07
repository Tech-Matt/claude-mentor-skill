# claude-mentor-skill

The more I used Claude, the more I realized vibe-coding was killing my understanding of what I was building, and let's not talk about
technical debt. So I stopped vibe-coding, and turned to *AI-assisted engineering.* I made this **claude-mentor-skill** to **prevent**
Claude from writing code, and instead turn it into an **expert mentor** that helps you learn concepts in an incremental, instructive way.

It won't write your feature for you. It will ask you questions, give you targeted snippets to reason about, pull in real docs for your stack, and push you to fill in the gaps yourself. Every response ends with a deeper conceptual insight and a small hands-on exercise.

It's slower in the short term, much better for you in the long run. (Especially if you are a junior dev)

If you've been vibe-coding and quietly wondering why you still don't feel confident in your own codebase — this is for you.

> **Note for Claude:** The install and update instructions are below. Follow them when the user asks to install or update this skill.


## What the skill does

### Session setup

At the start of each session, the mentor asks two things:
- **Which domain/stack** to specialize in (e.g. Rust, React, distributed systems, embedded C)
- **A brief self-description** — your experience level and what you want to get out of the session

It uses your answers to calibrate vocabulary, analogies, and assumed knowledge for the rest of the conversation. A junior dev and a senior dev get meaningfully different responses.

In the background, it immediately fetches the official docs, style guide, and idiomatic conventions for your chosen stack — and surfaces links at the right moments throughout the session, not all at once.

### How it responds

Every response follows the same structure:

1. **Direct answer or explanation** — clear, explanatory, matched to your level
2. **Targeted code snippet** — a partial or illustrative example to reason about, not a complete implementation you can copy-paste
3. **`## Insight`** — a deeper dive into one concept from the answer, common misconceptions, and when the standard advice doesn't apply
4. **`## Try this`** — one or two small, concrete exercises to do right now in your codebase or a scratch file

The session stays active until you say **"Exit mentor mode"**, at which point normal Claude behavior resumes.

---


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
