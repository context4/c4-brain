# Red-Team Review

Spawn hostile reviewers that try to break the plan, adjudicate their findings, and let the user decide what to apply.

## Plan resolution

1. Path argument, if given.
2. Otherwise the active plan (see SKILL.md, "Plan location & invariants").
3. Otherwise ask the user for a path, or offer to create a plan first.

## Workflow

1. **Read** `plan.md` and every `phase-*.md` in full.
2. **Scale reviewers** by phase count: 1-2 phases → Security Adversary + Assumption Destroyer; 3-5 → add Failure Mode Analyst; 6+ → all four lenses (`red-team-personas.md`).
3. **Run reviewers** in parallel as subagents if the runtime supports them, each with the prompt template from `red-team-personas.md`. Without subagents, run each lens yourself as a separate pass, re-reading the plan fresh each time.
4. **Collect**: deduplicate, sort Critical → High → Medium, cap at 15.
5. **Evidence filter**: a finding whose Evidence has no `path:line` citation is auto-rejected ("No repository evidence").
6. **Adjudicate** the rest: Accept or Reject, with a specific rationale.
7. **User review** — offer: apply accepted findings / review each one / reject all. When reviewing each, offer: apply / reject / modify (record the user's text verbatim; disposition "Accept (modified)").
8. **Apply** accepted findings to the target phase files and add `## Red Team Review` to `plan.md` (format in `red-team-personas.md`).
9. **Sweep**: run the Whole-Plan Consistency Sweep (`verification-roles.md`) and append it to `## Red Team Review`.
10. **Log**: append `## [YYYY-MM-DD] plan | Red-team: <title>` to `log.md`.

## Output

Findings by severity, accepted vs rejected, files modified, sweep results, key risks addressed.

## Next steps

Suggest `c4:plan validate <plan-dir>` before implementation. Do not call the plan ready while the sweep reports unresolved contradictions. When the user approves, the next step is to implement the plan phase by phase.
