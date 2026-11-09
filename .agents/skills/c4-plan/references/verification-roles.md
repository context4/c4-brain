# Verification Roles

Language-agnostic roles for checking a plan against the actual repository. Used while drafting (Fact Checker inline), during `validate`, and by red-team reviewers.

## Tiers (by phase count)

| Phases | Tier | Active roles | Budget |
|--------|------|--------------|--------|
| 1-2 | Light | Fact Checker | 5 claims/phase |
| 3-4 | Standard | Fact Checker + Contract Verifier | 10 claims/phase |
| 5+ | Full | All four | 15+ claims/phase |

## Fact Checker

Verify that every cited path, symbol, endpoint and config key exists.
- Glob for paths; grep for symbols, routes, config keys.
- Red flags: helper names grep cannot find; "central" modules that are actually scattered; paths renamed since scouting.
- Output per claim: `VERIFIED (file:line)` | `FAILED (not found)` | `UNVERIFIED (ambiguous)`.

## Flow Tracer

Verify behavioral claims ("X triggers Y", "A runs before B").
- Start at the entry point; read the real path through guards, branches and early returns.
- For async code, check ordering guarantees.
- Red flags: no shared call path; skipped intermediate steps; async treated as sync.
- Output: traced path with file:line, or FAILED with the actual flow.

## Scope Auditor

Verify new state (fields, singletons, env vars, context values) respects lifetimes.
- Find all instantiation sites; classify as request-, session- or process-scoped.
- Red flags: per-request data on a shared singleton; duplicate state under a new name.
- Output: lifetime with sites, or FAILED with the leak.

## Contract Verifier

Verify interface changes account for every consumer.
- Grep all callers and list them; never write "update all callers". Over 10: list 10, state the total.
- Check tests, imports, re-exports, configs, CI scripts, help text.
- Output: caller list with file:line, or FAILED with missing callers.

## Output format

```markdown
### Verification Results
- Tier: Light | Standard | Full
- Claims checked: N — Verified: N | Failed: N | Unverified: N

#### Failures
1. [Fact Checker] `src/utils/auth.ts` — not found; actual: `src/lib/auth.ts`
```

## Whole-Plan Consistency Sweep

Run after any edit from drafting, validation or red-team, so a fix in one phase does not leave stale claims in others.

1. Re-read `plan.md` and every `phase-*.md`.
2. List this session's decision deltas: renamed files, APIs, fields; changed decisions; changed order, dependencies, ownership or success criteria.
3. Search all plan files for old terms and superseded assumptions; update duplicated drafts (queries, commands, contracts) everywhere they appear.
4. Reconcile overview, phases table, requirements, steps, success criteria, risks and logs.
5. Check frontmatter fields and that every relative link resolves.
6. Unresolvable conflicts go to open questions; do not call the plan ready while any remain.

Append to the current `## Validation Log` or `## Red Team Review`:

```markdown
### Whole-Plan Consistency Sweep
- Files reread: plan.md, phase-01-…, phase-02-…
- Decision deltas checked: N — stale references fixed: N — unresolved: N
```
