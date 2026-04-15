Review the recent code changes (use git diff) with focus on:

1. **Correctness** — Does the code do what it's supposed to?
2. **Security** — Any injection, XSS, data exposure, or OWASP top 10 risks?
3. **Performance** — Unnecessary computation, missing caching, N+1 queries?
4. **Readability** — Is the intent clear? Naming appropriate? Overly complex?
5. **Test coverage** — Are important paths and edge cases covered?
6. **Consistency** — Does it follow the project's existing conventions (see CLAUDE.md)?

For each issue found, output:
- **Severity**: critical / warning / suggestion
- **Location**: file:line
- **Problem**: what's wrong
- **Fix**: how to fix it

If everything looks good, say so briefly.
