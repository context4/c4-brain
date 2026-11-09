# Save result (`--save`)

Persist the accepted brainstorm as a wiki synthesis. Write the page in the user's language.

1. **Page:** `wiki/<project>/syntheses/<slug>.md` (no current project — `wiki/general/syntheses/`) (kebab-case Latin slug). If a page with that slug exists, update it instead of duplicating.
2. **Frontmatter** (repository wiki format):
   ```yaml
   ---
   title: <title>
   type: synthesis
   tags: [brainstorm]
   project: <slug | general>
   sources: []      # wiki/<project>/sources/* or raw/<project>/* used as evidence
   projects: []     # related project name, if any
   created: YYYY-MM-DD
   updated: YYYY-MM-DD
   ---
   ```
3. **Body:** short summary; Outcome, Constraints, Non-goals, Acceptance criteria; Trade-offs and Better approaches when present; options considered; chosen direction and why; unresolved questions last. Link evidence with `[[wiki-links]]`.
4. **Project link:** with a current project, add the page to `wiki:` in its `project.yaml` and a `decisions.md` entry that links to it. Never create a project.
5. **Index:** add a line under the project's subsection (or `### general`) of `## Вики` in `index.md`: `- [[wiki/<project>/syntheses/<slug>]] — <one-line summary>`.
6. **Log:** append to the root `log.md` (and the project's `log.md`, if any): `## [YYYY-MM-DD] brainstorm | <title>` plus one line with the page path.

Use the local date (`date +%F`).
