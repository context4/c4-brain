# Research & Scouting

Skip whatever the user already supplied (research notes, file lists). Save findings to `{plan-dir}/reports/` so the plan can cite them.

## Codebase scouting

- Search with native file search (glob/grep) and read the matching files. For broad searches, split by area and run subagents in parallel if the runtime offers them; wait for all before analysis.
- Do not assume a fixed docs layout. Read the repository instructions (`CLAUDE.md`, `AGENTS.md`) and root README first, follow their navigation, and verify documented structure against current files.
- Record: existing patterns and conventions, configuration and dependencies, integration points, data flow, known debt or inconsistencies.

## External research

- Run up to 2 parallel research threads, each on one approach or question.
- Use web search and page fetching for current library docs, APIs and best practices. Prefer official docs; note the URL and date for every claim.
- GitHub context (issues, PRs, Actions logs) via `gh` when available; for another repository, read it with `gh` or a shallow `git clone` into a scratch directory.
- For a bug or failure, reproduce and trace the root cause before planning the fix.

## Practice

- Breadth before depth; identify several approaches before choosing.
- Note security implications and edge cases early.
- Separate verified facts from assumptions; tag unconfirmed claims `[UNVERIFIED]`.
