Analyze all uncommitted changes and create well-structured git commits.

## Process

1. **Scan**: Run `git status` and `git diff --stat`. Read the actual diff to understand what changed.

2. **Credential check**: Scan all staged and untracked files for API keys, tokens, passwords, private keys, or connection strings. If found, STOP and warn before any commit. Add the file to .gitignore if appropriate.

3. **Group**: Identify logical change groups. Common splits:
   - Feature work vs cleanup/refactor
   - Source code vs documentation
   - Application code vs config/CI changes
   - Independent bug fixes that happen to be in the same working tree

   If all changes are one logical unit, use a single commit. Don't split artificially.

4. **Present the plan**: Show a table of proposed commits with: commit order, files included, and draft message. Wait for user confirmation before committing.

5. **Execute**: For each commit:
   - Stage only the relevant files (never `git add -A` blindly)
   - Write a concise commit message: imperative mood, first line under 72 chars, body explains WHY not WHAT
   - Follow the project's existing commit style (check `git log --oneline -10`)

6. **Verify**: Run `git status` after all commits to confirm clean working tree (or show what's intentionally left uncommitted).

## Rules

- Never commit files that look like secrets (.env, credentials, key files, scratch files with tokens).
- Never amend existing commits unless the user explicitly asks.
- Never force push.
- If the project has a pre-commit hook, let it run. If it fails, fix the issue and create a NEW commit.
- Generated files (lockfiles, codegen) go with the commit that caused the regeneration, not in a separate commit.
