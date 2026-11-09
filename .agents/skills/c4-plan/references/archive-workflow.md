# Archive

Close finished or abandoned plans. Archiving changes status only; plan files stay on disk as history.

## Plan resolution

1. Path argument, if given.
2. Otherwise every `plan.md` under the plan root (the current project's `plans/`, else root `plans/`).

## Workflow

1. **Read** each `plan.md` and the first ~20 lines of each phase file to judge real progress (status fields and checkboxes).
2. **Propose**: list candidates (title, status, created, phases done/total) and ask the user to choose: all completed or cancelled plans, a specific selection, or cancel.
3. **Archive** each confirmed plan:
   - In `plan.md` frontmatter set `status: archived` and add `archived: YYYY-MM-DD`. Keep the earlier outcome visible in the body (one line: completed or cancelled, and why).
   - Append `## [YYYY-MM-DD] plan | Archived: <title>` to the project's `log.md` (if any) and the root `log.md`.
4. **Never delete** plan folders or files and never use `rm -rf`. Do not move plans unless the user explicitly asks. If the user wants a folder gone, they remove it themselves (`git rm -r <plan-dir>` keeps it in git history).
5. **Commit** (optional): ask whether to stage and commit, commit and push, or leave it. Use plain `git` with a conventional commit message.

## Output

Number of plans archived and a table: title, previous status, created, archived date.
