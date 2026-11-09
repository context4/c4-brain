# Validate

Verify the plan against the repository, then interview the user with critical questions before implementation starts.

## Plan resolution

1. Path argument, if given.
2. Otherwise the active plan (see SKILL.md, "Plan location & invariants").
3. Otherwise ask for a path, or offer `c4-plan --hard`.

## Workflow

1. **Read** `plan.md` and every `phase-*.md`; note decision points, assumptions, risks, trade-offs.
2. **Extract topics** using `validate-question-framework.md`.
3. **Verification pass** (`verification-roles.md`). If `## Red Team Review` already carries verification evidence, only resolve remaining `[UNVERIFIED]` tags.
   - Pick the tier by phase count; sample claims per the budget; verify with glob/grep.
   - Every FAILED claim becomes an interview question, with the found alternative as the recommended option. Never silently correct plan files.
   - Append Verification Results to `## Validation Log`.
4. **Generate questions**: 3-8 by default (fewer is fine for a simple plan), each with 2-4 concrete options, recommended one marked.
5. **Interview**: use the runtime's question tool if available, otherwise ask in chat; group related questions, at most 4 at a time.
6. **Document** answers in `## Validation Log` in `plan.md` (format in `validate-question-framework.md`).
7. **Propagate** decisions into affected phases; mark each edit `<!-- Updated: Validation Session N - {change} -->`.
8. **Sweep**: run the Whole-Plan Consistency Sweep and append it to the current Validation Log session. Ask the user about anything unresolved.
9. **Log**: append `## [YYYY-MM-DD] plan | Validated: <title>` to `log.md`.

## Output

Questions asked, decisions confirmed, phases updated, sweep results, recommendation: proceed or revise.

## Next steps

If verification shows `Failed: 0` and the sweep has no unresolved contradictions, the plan is ready: offer to implement it with `c4-cook`, ideally in a fresh session that is given the absolute path to `plan.md`. If anything failed, revise first.
