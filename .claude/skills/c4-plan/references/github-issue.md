# GitHub Issue (`--github`, optional)

After the red-team and validation gates (when they run):

1. Check `gh auth status` and that the repository has a GitHub remote. If not, report the reason and continue; the plan never depends on GitHub.
2. Create an issue titled `Plan: <title>`, or comment on the source issue if the task came from one. Body: objective, phases with one line each, total effort, repository-relative link to `plan.md`.
3. Add a `ready to review` label only if that label exists in the repository.
4. Write the issue number into `issue:` in `plan.md` frontmatter and include the URL in the handoff.

Never put secrets, private logs or absolute local paths into the issue.
