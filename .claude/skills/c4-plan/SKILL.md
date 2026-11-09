---
name: c4:plan
description: Create, validate, red-team or archive implementation plans with acceptance criteria and executable phases. Use for planning and roadmaps before implementation starts.
user-invocable: true
when_to_use: "Invoke when work needs phases, architecture, or a roadmap."
category: workflow
keywords: [planning, architecture, phases, roadmap, validation, red-team]
argument-hint: "[task] [--auto|--fast|--hard|--deep|--parallel|--two|--debate] [--tdd] [--yagni] [--no-tasks] [--github] OR [validate|red-team|archive] [plan-path]"
license: MIT
metadata:
  author: "c4-brain (adapted from AgentKit ak:plan, MIT)"
  version: "1.0.0"
---

# Plan (`c4:plan`)

Create structured, verifiable implementation plans: phased roadmap, file-level steps, success criteria and test commands. This skill plans only; it never implements.

This skill is self-contained. It uses only native capabilities: file search and read, shell, web search, `git`, optional `gh`, and subagents when the runtime offers them. When a capability is missing, do the same work sequentially yourself.

## Language

Write plan content (titles, prose, questions to the user) in the user's language — Russian if the user writes in Russian. Keep file names, frontmatter keys, code, paths and commands in English.

## Plan location & invariants

- All plans live under `plans/YYMMDD-HHMM-<slug>/` at the repository root (local time, `date +%y%m%d-%H%M`; slug in kebab-case Latin).
- Files: `plan.md` (index) and `phase-NN-<name>.md` (execution detail). Create them by hand; there is no scaffolding tool. Format: `references/plan-format.md`.
- **Active plan**: when a subcommand gets no path, read the frontmatter of every `plans/*/plan.md`; pick the one with `status: in-progress`, else the newest `pending`. If none or several match ambiguously, ask the user.
- Plan files are the source of truth. Runtime task lists are only a projection (`references/task-management.md`).

## Mode & subcommand routing

| Mode / subcommand | Flag / argument | Purpose | Reference |
|---|---|---|---|
| Auto-detect | (none) or `--auto` | Pick a mode from task complexity | `references/workflow-modes.md` |
| Fast | `--fast` | No research; direct analysis and plan | `references/workflow-modes.md` |
| Hard | `--hard` | Research, scouting, red-team, validation | `references/workflow-modes.md` |
| Deep | `--deep` | Per-phase scouting for large overhauls | `references/workflow-modes.md` |
| Parallel | `--parallel` | Phases with strictly disjoint file ownership | `references/workflow-modes.md` |
| Two approaches | `--two` | Two architectures with trade-offs; user picks | `references/workflow-modes.md` |
| Debate | `--debate` | Three independent candidate plans, synthesized | `references/workflow-modes.md` |
| Validate | `validate [path]` | Critical-question interview + verification pass | `references/validate-workflow.md` |
| Red-team | `red-team [path]` | Adversarial multi-lens review | `references/red-team-workflow.md` |
| Archive | `archive [path]` | Close finished plans without deleting files | `references/archive-workflow.md` |

### Modifiers

- `--tdd`: test-first design; every phase gets Tests Before / Refactor / Tests After and a regression gate (`references/plan-format.md`).
- `--yagni`: actively challenge and cut scope not needed for the stated outcome (`references/scope-challenge.md`). Without it, deliver the full requested scope.
- `--no-tasks`: skip mirroring phases into the runtime task list.
- `--github`: optional; create or update a GitHub issue via `gh` (`references/github-issue.md`).

### Mode exclusivity

`--auto`, `--fast`, `--hard`, `--deep`, `--parallel`, `--two`, `--debate` are mutually exclusive. Two mode flags is a hard stop: name both and ask which one. `--debate` is opt-in only and never auto-selected.

## Core rules

1. **Grounded decisions**: never infer architecture from file names; read the relevant code, configs and docs.
2. **KISS, full scope**: the smallest complete solution that delivers everything requested. Cutting scope requires `--yagni` or a direct user instruction.
3. **No placeholders**: real paths, real steps, runnable verification commands.
4. **File ownership**: `--parallel` phases declare disjoint file sets.
5. **Safety**: never put secrets, tokens or credentials in plans.

## Planning pipeline

Resolve flags first, then load only the references the selected route needs.

1. **Intake & scope challenge** — read context, restate scope (`references/scope-challenge.md`).
2. **Research & scouting** (hard/deep/two/debate) — `references/research-phase.md`.
3. **Draft** — design the solution (`references/solution-design.md`), then write `plan.md` and phase files (`references/plan-format.md`). Self-verify paths and symbols as you write (`references/verification-roles.md`, Fact Checker).
4. **Red-team gate** (when the mode requires it) — `references/red-team-workflow.md`.
5. **Validation gate** (when the mode requires it) — `references/validate-workflow.md`.
6. **Whole-plan sweep** — check links, frontmatter and cross-phase consistency (`references/verification-roles.md`).
7. **Repository integration** — see below.
8. **Tasks** — mirror phases unless `--no-tasks` (`references/task-management.md`).
9. **GitHub** (if `--github`) — `references/github-issue.md`.
10. **Handoff** — `references/post-plan-handoff.md`.

## Repository integration

- **Project link.** Check whether the plan belongs to an existing project: list `projects/*/README.md` and match by goal and topic. If one clearly matches, set `project: <name>` in `plan.md` frontmatter and add a link to the plan under the `## Планы` heading of `projects/<name>/README.md` (add that heading if the README lacks it): `- [<title>](../../plans/<plan-dir>/plan.md) — <status>`. If the match is uncertain, ask.
- **Never create a project.** If no project matches, leave `project:` empty. If the work looks like a new project, suggest one line: «Похоже на отдельный проект. Завести через `c4:project`?» — and continue without it.
- **Log.** Append to the root `log.md` (append-only): `## [YYYY-MM-DD] plan | <title>` plus one line with the plan path. Validate, red-team and archive also append a line in the same format (`plan | Validated: <title>`, and so on).

## References

- `references/workflow-modes.md` — auto-detection and every mode, including debate
- `references/scope-challenge.md` — step 0: what exists, what was asked, complexity check
- `references/research-phase.md` — research, codebase scouting, docs lookup
- `references/solution-design.md` — trade-offs, load-bearing assumptions, risks
- `references/plan-format.md` — directory layout, frontmatter, plan and phase templates
- `references/verification-roles.md` — fact checking and whole-plan consistency sweep
- `references/red-team-workflow.md` — red-team procedure
- `references/red-team-personas.md` — reviewer lenses and prompt template
- `references/validate-workflow.md` — validation procedure
- `references/validate-question-framework.md` — question categories and log format
- `references/archive-workflow.md` — closing and archiving plans
- `references/task-management.md` — mirroring phases into a runtime task list
- `references/github-issue.md` — optional GitHub issue via `gh`
- `references/post-plan-handoff.md` — final report and next step
