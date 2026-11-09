# Solution Design

## Principles

- **Full requested scope** — design for everything asked; add nothing unrequested.
- **KISS** and **DRY**.
- With `--yagni`, also apply YAGNI: cut anything not needed for the stated outcome.

## Trade-offs

- Compare approaches per requirement, including their worst plausible case, not only the expected one.
- Weigh short- vs long-term cost, complexity vs maintainability, effort vs benefit.
- Recommend one approach and say why.

## Load-bearing assumptions

- List only the assumptions the design fails without.
- Resolve those that a read of source, tests or live state can settle; carry the rest forward.
- State the condition under which the design stops meeting its success criteria.
- When an assumption stays open, prefer the design that is cheapest to switch away from; note lock-in.
- In the phase's Risk Assessment, record the observable signal that the assumption broke and the pre-decided response (adjust, or stop and replan).

## Checklist

- **Security**: auth and authorization, data protection, input validation, secret handling.
- **Performance**: bottlenecks, caching, resource use, async work where it helps.
- **Failure modes**: errors, partial failure, retries and fallbacks, data consistency, races, graceful degradation.
- **Architecture**: component boundaries, data flow, contracts, state.
- **Operations**: testing strategy, monitoring, deployment and rollback.

Record decisions and their rationale in the plan.
