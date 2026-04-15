Systematically diagnose and fix the bug or error described by the user.

## Process

1. **Reproduce**: Understand the exact error. Read the full error message, stack trace, or user description. If a command can reproduce it, run it to confirm.

2. **Locate**: Trace from the error back to the root cause.
   - Follow the stack trace to the originating line
   - Read the surrounding code to understand intent
   - Check recent changes (`git diff`, `git log -5 -- <file>`) — was this working before?
   - Search for similar patterns elsewhere that DON'T fail — what's different?

3. **Diagnose**: State the root cause in one sentence before writing any fix. If uncertain, list the top 2-3 hypotheses ranked by likelihood and describe how to confirm each one.

4. **Fix**: Make the minimal change that addresses the root cause. Do not refactor surrounding code, add features, or "improve" things unrelated to the bug.

5. **Verify**: Run the failing command/test again to confirm the fix. If the project has a test suite, run it to check for regressions.

6. **Explain**: Briefly tell the user what went wrong and why, so they can recognize the pattern next time.

## Rules

- Never guess-and-check blindly. Read the error, form a hypothesis, then verify.
- If the first fix attempt fails, re-read the error output — don't retry the same approach.
- If the bug is in a dependency (not user code), say so. Don't patch around library bugs without flagging it.
- If the fix reveals a deeper design problem, mention it but don't fix it now. One bug at a time.
