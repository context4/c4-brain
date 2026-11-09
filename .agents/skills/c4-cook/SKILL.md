---
name: c4-cook
description: "Implement a plan phase by phase — or a small, clearly scoped change directly — with verification after every phase and progress written back into the plan files. Use after c4-plan, or when the user says \"делай\", \"реализуй\", \"погнали по плану\". Invoke to implement known scope: an existing plan, or a small change whose outcome is already clear."
license: MIT
metadata:
  author: c4-brain
  version: "1.0.0"
---

# Cook (`c4-cook`)

Turn an accepted plan into working, verified changes. Talk to the user in their language; keep file names, code and commands as they are.

## Pick the route

| Situation | Route |
|---|---|
| Path to a plan given, or an `in-progress` plan exists under the plan root | **Plan route** |
| Several candidate plans | List them (title, status, created) and ask which one |
| Small change, outcome clear (a few files, no design choice) | **Direct route** |
| Outcome unclear or there are real alternatives | Stop: suggest `c4-brainstorm`, then `c4-plan` |
| Large change without a plan | Stop: suggest `c4-plan` first |

Plan root: the current project's `projects/<slug>/plans/`, else root `plans/` (see «Текущий проект сессии» in `AGENTS.md`; if the project is unclear, ask «С каким проектом работаем?»). To find the active plan, read the frontmatter of every `plan.md` there; take `in-progress` first, then the newest `pending`.

## Plan route

1. **Load.** Read `plan.md` and every phase file. If the plan has `project:`, read that project's `project.yaml`, `README.md` and `decisions.md` too — its goal, non-goals and past decisions constrain the work. Files the work produces go to the project's `outputs/` (results) or `assets/` (inputs), never loose in the project root. Check the plan's open questions; if any block phase 1, ask before touching files.
2. **Mark start.** Set `status: in-progress` in `plan.md` frontmatter.
3. **For each phase, in dependency order:**
   1. **Re-scout.** Quick `c4-scout` pass over the phase's Files list: do the paths and symbols still exist as the plan says? If reality differs, adjust the steps and note the deviation in the phase file under `## Deviations`. If the difference changes the design, stop and ask.
   2. **Mark** the phase `status: in-progress` (phase frontmatter and the table in `plan.md`).
   3. **Do the Steps.** Touch only the files the phase lists (for `--parallel` plans, only its Owned files). Follow the repo's own conventions. No placeholders, fake data or disabled checks to make something pass.
   4. **Verify.** Run every command in the phase's Verification section and check each Success criterion. If something fails: find the cause, fix it, re-run. After three failed attempts on the same problem, stop and report what you tried — do not weaken the test.
   5. **Close the phase.** Tick the Todo checkboxes, set the phase `status: completed`, update the table in `plan.md`.
   6. **Checkpoint.** Report in 2–4 lines: what changed, what was verified, what is next. Without `--auto`, wait for the user's go-ahead before the next phase. With `--auto`, continue unless a verification failed or a design question came up.
4. **Finish.**
   - Run the broadest check the repo has (tests, lint, build), or explain why there is none.
   - Review your own diff once against the plan's overview and acceptance criteria: anything missing, anything extra?
   - Set `plan.md` `status: completed`.
   - If the plan has a project: tick or add the related Next actions in its `README.md`, set `updated` in `project.yaml`, record any decision taken during the work in `decisions.md`.
   - Append `## [YYYY-MM-DD] cook | <plan title>` plus one line with the result to the project's `log.md` (if any) and one line to the root `log.md`.
   - Commit only if the user asks, with a conventional commit message.

`--phase N` runs only that phase (its dependencies must be completed).

## Direct route

For small, clear changes without a plan:
1. State the outcome and acceptance criterion in one or two sentences; if the user has not confirmed them and they are not obvious, ask once.
2. `c4-scout` the affected area.
3. Make the change, run the narrowest useful check, then the broader one if shared behaviour changed.
4. Report what changed and how it was verified. Log it in `log.md` only if it changed the brain's structure or rules.

## Rules

- Never edit `raw/`. Never create a project — if the work turns out to be a new project, suggest `c4-project` in one line.
- Do not silently change scope. Anything you skipped, deferred or could not verify goes into the final report explicitly.
- Do not reverse a decision recorded in the plan, the project README or `decisions.md` without asking.
- Stop and ask on: destructive actions (deleting data, force-pushing, dropping tables), secrets, anything outward-facing (publishing, sending, deploying).
