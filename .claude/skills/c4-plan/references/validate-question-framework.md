# Validation Question Framework

## Categories

| Category | Signals in the plan |
|----------|---------------------|
| Architecture | approach, pattern, design, structure, database, API |
| Assumptions | assume, expect, should, will, must, default |
| Trade-offs | vs, alternative, option, either/or |
| Risks | risk, might, could fail, dependency, blocker |
| Scope | phase, MVP, future, out of scope, nice to have |

## Question rules

- 2-4 concrete options; mark the recommended one "(Recommended)"; free-text "Other" is always allowed.
- Surface implicit decisions; prefer questions that would change implementation.

Example — Assumptions: "The plan assumes no rate limiting is needed. Correct?" Options: Yes, not needed now | No, add basic limiting now (Recommended) | Defer to phase 2.

## Validation Log format

```markdown
## Validation Log

### Session N — YYYY-MM-DD
Trigger: {what prompted validation} · Questions: {count}

1. **[Category]** {full question text}
   - Options: A | B | C
   - Answer: {choice}
   - Custom input: {verbatim, if any}
   - Rationale: {why it matters for implementation}

#### Confirmed decisions
- {decision}: {choice} — {why}

#### Action items
- [ ] {change}

#### Impact on phases
- Phase N: {what changes and why}
```

Record the exact question text, every option, custom input verbatim; increment session numbers.

## Where decisions land

| Change type | Phase section |
|-------------|---------------|
| Requirements | Requirements |
| Architecture | Architecture |
| Scope | Goal / Steps |
| Risk | Risks |
| Other | Context |
