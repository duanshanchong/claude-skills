Audit the user's Claude Code setup and surface tips they might not know.

## Process

1. **Check current setup**:
   - Read `~/.claude/CLAUDE.md` (user-level instructions)
   - Read `~/.claude/settings.json` (permissions, hooks, env vars)
   - List `~/.claude/commands/` (available skills)
   - Read the project-level `CLAUDE.md` if it exists
   - Read the project-level `.claude/settings.json` if it exists
   - Check for MCP servers (`.mcp.json` or settings)
   - Check for hooks configuration

2. **Fetch latest Claude Code updates**: Search the web for recent Claude Code release notes, new features, and best practices. Focus on:
   - New capabilities added in recent releases
   - Popular community tips and workflows
   - Any breaking changes or deprecations

3. **Generate personalized tips** in three categories:

   **You're not using these yet** — Features that exist in Claude Code but aren't in the user's config:
   - Missing hooks that could automate repetitive tasks
   - Permissions that could be pre-allowed to reduce friction
   - MCP servers that would be useful for their project type
   - Settings they haven't customized (compaction, model preferences, etc.)

   **You could improve these** — Things in the config that could be better:
   - Skills that could be more effective with small prompt tweaks
   - CLAUDE.md instructions that are too vague or too restrictive
   - Permissions that are too broad or too narrow

   **What's new** — Recent Claude Code features or changes the user should know about, based on web search results.

4. **Present as a short, actionable list** — no more than 10 tips total. Each tip should be one sentence + one concrete action (a command to run, a file to edit, a setting to change).

## Rules

- Don't repeat things the user clearly already knows (check their setup first).
- Prioritize high-impact, low-effort tips.
- If there's nothing to improve, say so — don't manufacture tips.
