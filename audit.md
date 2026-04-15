Act as a FAANG Staff Engineer performing a pre-acquisition technical audit of this repository.

Execute the following phases in order. After each phase, pause briefly to let the user review before continuing. If the user says to skip a phase, move to the next one.

## Phase 1: Understand the Repository

Read every source file, config, CI pipeline, and doc. Use parallel Explore agents for speed. Do NOT start making judgments yet — just build a complete mental model.

Deliverable: Confirm you've read every file. List the tech stack, directory structure, and key architectural decisions in a brief summary.

## Phase 2: Audit (Do NOT Fix Anything)

Analyze six dimensions:
1. **Architectural risks** — god objects, tight coupling, missing abstractions, unmaintained dependencies
2. **Security** — leaked secrets (check git history too), missing auth, OWASP issues, compliance gaps (COPPA if children's app)
3. **Dead code** — unused files, methods, strings, assets. Verify each with whole-repo grep (including tests).
4. **Code quality** — SRP violations, error handling gaps, resource leaks, files over 500 lines
5. **Test coverage** — what's tested, what's not, ratio of test LOC to source LOC
6. **Maintainability** — dependency graph, circular imports, constructor parameter counts, onboarding difficulty

For every finding, include: **file path, line number, severity (critical/high/medium/low), and evidence.**

## Phase 3: Rank All Issues

Produce a single ranked table with columns:
- **Tier** (0=blocker, 1=high, 2=moderate, 3=low)
- **Issue** (one-line description)
- **Business Risk** (what breaks if ignored)
- **Fix Effort** (hours/days)
- **ROI** (risk reduction per hour invested)

Sort by Tier ascending, then ROI descending within each tier. This table is the primary deliverable of the audit.

## Phase 4: Propose Target Architecture

Design the architecture you would build if starting from scratch today, while retaining what the current codebase got right. For each change:
- **What** changes (concrete: library names, directory structure, code patterns)
- **Why** the current approach fails
- **Migration path** from current → target (no big-bang rewrites; each phase ships a working app)

Include a dependency comparison table (current vs proposed) and estimated total migration effort.

## Phase 5: Safe Deletion Plan

Identify components that can be deleted with near-zero risk. Criteria:
- Dead files: defined but never imported anywhere
- Dead methods: defined but never called outside their own file
- Dead strings/constants: defined but never referenced outside their own file

Verify EVERY candidate with grep across the entire repo (lib/, test/, integration_test/, docs/). Exclude anything referenced in tests — even if the test is broken, it's not zero-risk.

For each candidate, list: file, line(s), evidence of non-use, and what replaced it.

## Phase 6: Execute and Self-Review

If the user approves the deletion plan:
1. Execute deletions in dependency-safe order
2. Run static analysis (`flutter analyze` or language equivalent)
3. Run tests
4. If a test fails, determine whether it's pre-existing or caused by the deletions
5. Write a critical self-review: what went right, what was risky, what you'd do differently

## Rules Throughout

- **Never modify code during Phases 1-4.** Audit only.
- Parallelize research with background agents. Don't duplicate their work.
- Every claim must have a file path and line number.
- If you find secrets in git history, flag immediately — don't wait for the report.
- Speak in specifics, not generalities. "The sync engine lacks error handling" is bad. "`root_shell.dart:168` — `saveStory().then(...)` has no `.catchError()`" is good.
