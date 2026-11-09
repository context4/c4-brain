---
name: c4-brainstorm
description: "Turn unclear intent into an accepted outcome (outcome, constraints, non-goals, acceptance criteria) and compare 2-3 viable approaches before delivery. Use at the opening of multi-step work, or when a diagnosed problem has meaningful solution choices. Options: --ask (interview), --save (save result to the wiki), --yagni (cut scope)."
license: MIT
metadata:
  author: "c4-brain (adapted from AgentKit ak:brainstorm, MIT)"
  version: "1.0.0"
---

# Brainstorm (`c4-brainstorm`)

Turn incomplete intent into a bounded, accepted outcome. Stay honest about evidence, trade-offs and uncertainty without turning a clear request into a ceremonial interview. This skill shapes intent and choices; it never implements.

## Language

Hold the conversation and write any saved output in the user's language — Russian if the user writes in Russian. Keep file names, frontmatter keys, paths and commands in English.

## Brainstorm contract

Every multi-step delivery starts by capturing:

- **Outcome:** the user-visible or operational end state.
- **Constraints:** safety, compatibility, time, technology and ownership boundaries.
- **Non-goals:** nearby work this delivery will not absorb.
- **Acceptance criteria:** observable evidence that proves completion.

Conditional fields — include only when the condition holds, never as `N/A` placeholders:

- **Trade-offs:** whenever two or more approaches were compared. For each, name the assumption it depends on most and the condition under which it fails first.
- **Better approaches:** when inspection surfaced something better than what the user proposed — give the evidence, the practical difference and the cost of switching. If options were compared and nothing better was found, write `Better approaches: none — the requested direction holds (<evidence>)`.

An accepted plan or design that already records the four fields satisfies the contract. Reuse it and raise only material gaps; never make the user repeat settled decisions.

## Proportional behavior

- Concrete request: summarize the four fields briefly and continue.
- Ask only when a missing answer would materially change the result or a safety boundary and cannot be discovered. **One question at a time**; wait for the answer before the next.
- Separate what can be discovered (files, wiki pages, project READMEs, plans) from what cannot (the user's goals, future requirements, audience response). Resolve the first by reading — use `c4-scout` or subagents, if the runtime offers them, for broad discovery — and ask only about the second. Never invent the user's goals; mark unknowns `❓ не выяснено`.
- Direct answers and read-only lookups need no brainstorm. If investigation turns into changing files, satisfy the contract first.

## Brain integration

- **Current project.** Use the session's current project (see «Текущий проект сессии» in `AGENTS.md`); if it is unclear and the topic may belong to one, ask «С каким проектом работаем?». With a project, read its `project.yaml`, `README.md`, `interview.md` and `decisions.md` before anything else; reuse its goal and done-criterion as constraints. The chosen approach is recorded in the project's `decisions.md` (date, decision, why, options considered).
- **Never create a project.** If the idea looks like a new project, say one line: «Похоже на отдельный проект. Завести через `c4-project`?» — and continue without it.
- **Wiki context.** Read `index.md` and only the wiki pages relevant to the topic; cite them as evidence.

## Bugs and failures

Frame the expected repaired behavior, constraints, non-goals and acceptance evidence first. Do not propose fixes from the symptom: locate the failing path, prove the root cause, then compare cause-aligned fixes only if more than one is viable. Otherwise record why the direct fix is enough.

## Option exploration

When the work has a real design choice:

1. Inspect the smallest relevant set of files, wiki pages and existing plans.
2. State confirmed constraints and any evidence gaps.
3. Present 2–3 viable approaches with trade-offs. For each, name its load-bearing assumption and its first failure condition; compare on the worst plausible case, not only the best.
4. Recommend the smallest approach that satisfies the contract. When a load-bearing assumption cannot be resolved now, prefer the approach that is cheapest to abandon.
5. Ask the user to pick. Resolve material disagreement before any delivery starts.

Apply KISS and DRY. Deliver the full requested scope — never trim what the user asked for, and do not invent extra components to make a design look complete. With `--yagni`, additionally challenge and cut scope not needed for the stated outcome.

## Flags

| Flag | Behavior |
|---|---|
| `--ask` | Evidence-first interview before finalizing the contract — `references/interview-mode.md`. Never forwarded downstream. |
| `--save` | Save the accepted result as a wiki synthesis — `references/save-result.md`. |
| `--yagni` | Scope-cutting opt-in; forward it to the next skill. |

Without `--save`, offer saving in one line only when the decision should outlive the session; never save just to satisfy the contract.

## Handoff

Pass the contract fields (with Trade-offs and Better approaches when present), the chosen direction, evidence and open risks to the next step:

- delivery follows: suggest `c4-plan` — it reuses the accepted outcome, constraints, non-goals and acceptance criteria; implementation then goes through `c4-cook`;
- exploration only: report the recommendation and stop.

Include `--yagni` in the handoff only if the user passed it.

## Boundaries

- Never claim current behavior from intent alone.
- Never edit `raw/`; never expose secrets or unrelated private files.
- List unresolved questions last.

## References

- `references/interview-mode.md` — `--ask`: evidence-first, one-question-at-a-time interview
- `references/save-result.md` — `--save`: wiki synthesis page, `index.md` and `log.md` entries
