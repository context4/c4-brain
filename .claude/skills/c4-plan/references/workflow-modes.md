# Workflow Modes

## Auto-detection (default, or `--auto`)

| Signal | Mode |
|--------|------|
| Simple task, clear scope, no unknowns | fast |
| Complex task, unfamiliar domain, new tech | hard |
| Major refactor, 5+ areas, architectural debt | deep |
| 3+ independent features, layers or modules | parallel |
| Ambiguous approach, several valid paths | two |

Ask the user if detection is uncertain. `debate` is never a detection outcome.

Step 0 (`scope-challenge.md`) runs before detection. Under `--yagni`, EXPANSION suggests `hard` or `two`, REDUCTION suggests `fast`. Explicit mode flags always win. `--fast` changes planning depth, never the requested scope.

## Fast (`--fast`)

Analyze → plan → tasks.

1. Read repository instructions and docs navigation; confirm against relevant source and tests.
2. Write the plan (`plan-format.md`).
3. Mirror tasks unless `--no-tasks`.

## Hard (`--hard`)

Research → scout → plan → red-team → validate → tasks.

1. Run up to 2 research threads in parallel (subagents if available) — `research-phase.md`.
2. Scout the codebase where owning evidence is missing or ambiguous.
3. Write the plan from the collected research notes.
4. Red-team (`red-team-workflow.md`), then validate (`validate-workflow.md`).
5. Mirror tasks unless `--no-tasks`.

## Deep (`--deep`)

For large overhauls.

1. Research and scout phase 1 in depth.
2. Plan phase 1 in detail; outline phases 2+.
3. Each later phase states that it needs its own scouting pass right before implementation.
4. Add file inventory, scenario matrix and dependency map (`plan-format.md`).
5. Red-team and validate.

## Parallel (`--parallel`)

1. Design a decoupled modular architecture.
2. Split into phases with strictly disjoint file ownership; list owned files in each phase.
3. Mark which phases can run concurrently and where they integrate.
4. Red-team and validate.

## Two approaches (`--two`)

1. Research two genuinely different approaches.
2. Draft both architectures and a trade-off matrix (effort, risk, worst case, reversibility).
3. Present them to the user and wait for a choice.
4. Write the full plan for the chosen approach; record the rejected one briefly under "Alternatives considered".

## Debate (`--debate`)

Shared evidence → 3 independent candidate plans → one synthesized plan → red-team → validate → tasks.

1. Build a shared evidence packet with the same research as `--hard`; save it to `{plan-dir}/reports/debate-evidence.md`.
2. Produce 3 candidate plans independently, without cross-reading: 3 parallel subagents if available, otherwise 3 sequential drafts that each start from the evidence packet only. Save to `{plan-dir}/reports/candidate-{N}.md`.
3. If a candidate is unusable, redo it once.
4. Synthesize one plan: record consensus, disagreements and the reason each disagreement was resolved; write `plan.md` and phase files.
5. Run the red-team and validation gates.
