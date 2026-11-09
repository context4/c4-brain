# Plan Format

## Directory layout

```
<plan root>/YYMMDD-HHMM-<slug>/   # projects/<project>/plans/ or root plans/
├── plan.md                      # index: frontmatter, overview, phases table
├── phase-01-<name>.md           # one file per phase
├── phase-02-<name>.md
└── reports/                     # optional: research, scouting, debate candidates
```

Create the directory and files by hand. Before writing, check the plan root for an existing plan on the same topic; extend it instead of duplicating, and note related plans in `blockedBy` / `blocks`.

## plan.md frontmatter (required)

```yaml
---
title: "Brief plan title"
description: "One-sentence summary"
status: pending        # pending | in-progress | completed | cancelled | archived
priority: P2           # P1 high | P2 medium | P3 low
effort: 4h             # sum of phase estimates
project: ""            # slug of the current project, else empty
issue: ""              # GitHub issue number, if any
branch: ""             # `git branch --show-current`, if in a git repo
tags: []               # e.g. feature, bugfix, refactor, docs, infra, content
blockedBy: []          # other plan dir names
blocks: []
created: YYYY-MM-DD
---
```

Auto-fill: `title` from the task, `description` from the overview's first sentence, `status: pending`, `priority` from the request or P2, `created` today. Missing referenced plans produce a warning, not a block.

## plan.md body (keep under ~80 lines)

```markdown
# <Title>

## Overview
What this plan achieves and why.

## Phases
| Phase | Name | Status |
|-------|------|--------|
| 1 | [Setup environment](./phase-01-setup-environment.md) | pending |
| 2 | [Core implementation](./phase-02-core-implementation.md) | pending |

## Dependencies
Key external and cross-plan dependencies.

## Not in scope
Only when items were explicitly deferred.

## Open questions
Or "None".
```

Link text in the phases table is a human-readable name, not a file name. Update the table by hand when a phase status changes.

## Phase file template

```markdown
---
phase: 1
title: "Phase name"
status: pending        # pending | in-progress | completed
priority: P2
effort: "2h"
dependencies: []       # phase numbers this one waits for
---

# Phase 1: <Name>

## Goal
One sentence: the observable outcome.

## Context
Links to related reports, files, docs, wiki pages.

## Requirements
Functional and non-functional.

## Architecture
Design, component interactions, data flow (only when relevant).

## Files
- Create: `path/to/file`
- Modify: `path/to/existing` — what changes
- Delete: `path/to/old`

## Steps
1. Concrete, numbered actions with exact paths and symbols.

## Todo
- [ ] Checkbox per deliverable

## Success criteria
Definition of done, stated as something observable.

## Verification
- `command` — expected result (exit code, output substring, file that must exist)

## Risks
Issue → mitigation; signals for broken assumptions and the pre-decided response.

## Security
Auth, data protection, secrets (only when relevant).
```

Small phases may drop empty sections. Never drop Goal, Files, Steps, Success criteria, Verification.

## Mode extensions

- `--deep`: add a file inventory table (action, rough size, test impact), a test scenario matrix (critical / high / medium paths), and a dependency map to other phases.
- `--tdd`: add **Tests Before** (regression coverage written first), **Refactor** (protected changes), **Tests After** (new behavior) and a **Regression gate** with the exact command that must pass.
- `--parallel`: add **Owned files** — the only files this phase may touch.

## Writing quality

- Lead with the outcome; complete sentences, bullets, no filler.
- Every task independently executable, with exact paths and clear acceptance criteria.
- Detailed enough for a less experienced executor; code snippets or pseudocode where they remove ambiguity.
- Order by dependencies, then risk, then value.
- Follow the repository's own instructions and standards; do not assume a fixed docs path.
- End by asking the user about unresolved questions (decisions, unknowns, business trade-offs), then revise the plan with the answers.
