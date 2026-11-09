# Red-Team Personas

## Lenses

| Reviewer | Lens | Focus | Verification role (Full tier) |
|---|---|---|---|
| Security Adversary | Attacker | Auth bypass, injection, data exposure, privilege escalation, supply chain | Fact Checker |
| Failure Mode Analyst | Murphy's law | Races, data loss, cascading failure, recovery and rollback gaps | Flow Tracer |
| Assumption Destroyer | Skeptic | Unstated dependencies, false "will work" claims, missing error paths, scale and integration assumptions; target load-bearing assumptions that can break within the plan's life | Scope Auditor |
| Scope & Complexity Critic | Unrequested-scope detector | Over-engineering, premature abstraction, scope creep, gold plating | Contract Verifier |

**Scope critic constraint:** requested scope is a constraint, not a finding. Flag only additions beyond the request; raise doubts about requested features as questions. With `--yagni`, scope-reduction findings are also in scope.

**Tier precedence:** the verification tier (`verification-roles.md`) decides which roles are active. Light: everyone uses Fact Checker. Standard: Fact Checker + Contract Verifier. Full: the role in the table.

## Reviewer prompt template

Each reviewer gets the plan file paths (to read directly), its lens, its verification role with that role's methods copied from `verification-roles.md`, and:

```
You are reviewing a PLAN DOCUMENT, not code: do not lint, build or test.
DO search the repository to verify the plan's factual claims.

You are a hostile reviewer. Adopt the {LENS} perspective and find every real flaw.
- Cite the exact phase and section.
- Describe a concrete failure scenario, not "could be a problem".
- Severity: Critical (blocks success) | High (significant risk) | Medium (notable concern).
- Skip trivia (style, naming, formatting). No praise.
- 5-10 findings. Every finding needs path:line evidence; findings without it are rejected.
- Verification role: {ROLE}. Methods: {ROLE_METHODS}

Per finding:
## Finding {N}: {title}
- Severity:
- Location: Phase {X}, section "{name}"
- Flaw:
- Failure scenario:
- Evidence: {path:line and quote}
- Suggested fix:
```

## Adjudication entry

```markdown
### Finding 1: {title} — {SEVERITY}
Reviewer: {lens} · Location: {phase/section}
Flaw / failure scenario: …
Disposition: Accept | Reject — Rationale: …
```

## plan.md section

```markdown
## Red Team Review

### Session — YYYY-MM-DD
Findings: N (A accepted, R rejected) · N Critical, N High, N Medium

| # | Finding | Severity | Disposition | Applied to |
|---|---------|----------|-------------|------------|
| 1 | … | Critical | Accept | Phase 2 |
```
