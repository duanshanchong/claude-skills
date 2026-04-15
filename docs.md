Consolidate and sync the docs/ directory (or equivalent documentation location) with the current codebase.

## Process

1. **Inventory**: List every doc file with line count and one-line summary of what it covers.

2. **Assess each file** against the current code. For each doc, verdict one of:
   - **Keep** — accurate and not duplicated elsewhere
   - **Update** — partially stale, worth fixing
   - **Merge** — overlaps with another doc, combine into the stronger one
   - **Delete** — fully outdated, derivable from code, or historical (captured in git log)

   Present the verdict as a table before making any changes. Wait for user confirmation.

3. **Execute**:
   - Delete files marked Delete
   - Merge files marked Merge (absorb content into target, then delete source)
   - Rewrite files marked Update to reflect current code — read the actual source files, don't guess
   - Update the index/README if one exists

4. **Scrub for leaked secrets**: Check all remaining docs for hardcoded API keys, tokens, passwords, or connection strings. Replace with placeholders.

5. **Verify**: Run static analysis to confirm no code references to deleted doc files. Commit with a clear summary of what was consolidated and why.

## Rules

- Every deletion must be justified (outdated, redundant, or derivable from code).
- Never delete operational docs (deploy guides, runbooks) unless truly obsolete.
- Never delete forward-looking docs (roadmaps, RFCs) — they capture intent not in code.
- If a doc's content is 100% derivable from source files, prefer deletion over maintenance burden.
- Aim to minimize total doc count while preserving non-obvious knowledge.
