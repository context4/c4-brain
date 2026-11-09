# Save result (`--save`)

Persist the accepted brainstorm as a wiki synthesis. Write the page in the user's language.

1. **Page:** `wiki/syntheses/<slug>.md` (kebab-case Latin slug). If a page with that slug exists, update it instead of duplicating.
2. **Frontmatter** (repository wiki format):
   ```yaml
   ---
   title: <title>
   type: synthesis
   tags: [brainstorm]
   sources: []      # wiki/sources/* or raw/* pages used as evidence
   projects: []     # related project name, if any
   created: YYYY-MM-DD
   updated: YYYY-MM-DD
   ---
   ```
3. **Body:** short summary; Outcome, Constraints, Non-goals, Acceptance criteria; Trade-offs and Better approaches when present; options considered; chosen direction and why; unresolved questions last. Link evidence with `[[wiki-links]]`.
4. **Project link:** if the brainstorm belongs to an existing project, add a link to the page in `projects/<name>/README.md`. Never create a project.
5. **Index:** add a line under `## Синтезы` in `index.md`: `- [[wiki/syntheses/<slug>]] — <one-line summary>` (replace the `_Пусто._` placeholder if present).
6. **Log:** append to `log.md`: `## [YYYY-MM-DD] brainstorm | <title>` plus one line with the page path.

Use the local date (`date +%F`).
