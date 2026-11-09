# Step 0: Scope Challenge

Run before research or design.

## Skip when

- The task is trivial (single-file fix, typo, config change).
- The user signals urgency ("just plan it", "quickly").
- The task is short and unambiguous.

Skipping preserves the full requested scope. Only `--yagni` or a direct instruction to cut a named item authorizes reduction.

## Three questions

1. **What already exists?** Search for code, utilities, notes or patterns that already solve part of the problem. Flag any plan step that would rebuild something present.
2. **What did the user actually ask for?** Restate the requested scope; it is the baseline the plan delivers in full. Flag additions beyond it. Note deferrable work as information only.
3. **Complexity check.** More than 8 files touched, more than 2 new services or classes, or more than 3 phases — challenge each and justify it.

## Scope modes (only with `--yagni`)

Ask the user to choose, recommending C:

| Option | Mode | Meaning |
|---|---|---|
| A | EXPANSION | Explore the ambitious version, research deeper |
| B | HOLD | Scope is right; focus on execution, edge cases, tests |
| C | REDUCTION | Strip to essentials; defer everything non-blocking |

Still surface EXPANSION if analysis found missing scope that blocks the goal.

Without `--yagni`: do not present the fork. Record HOLD, reject only unrequested additions, deliver the full scope.

After a choice: EXPANSION — consider `--hard`/`--two`, label stretch items. HOLD — keep scope exactly. REDUCTION — minimal version, list deferred items under "Not in scope".

**Respect the choice.** Raise scope concerns once, here. Do not re-argue later.

## Output

```
Scope Challenge:
- Existing: [reusable code or notes found]
- Requested scope: [delivered in full unless REDUCTION]
- Complexity: [files, new abstractions]
- Mode: [EXPANSION | HOLD | REDUCTION]
```
