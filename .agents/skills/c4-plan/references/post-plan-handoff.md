# Post-Plan Handoff

Always end with an explicit handoff, in the user's language:

```markdown
### Plan
- Path: `plans/<plan-dir>/plan.md`
- Project: `<name>` (linked in `projects/<name>/README.md`) — or "none"
- Status: ready for implementation | needs revision (why)
- Phases:
  1. <Phase 1 title> — <one line>
  2. <Phase 2 title> — <one line>
- Open questions: <list or "none">

### Next step
Implement with `c4-cook plans/<plan-dir>` — it runs the plan phase by phase, verifies each phase and writes progress back into the plan files.
Optional before that: `c4-plan validate plans/<plan-dir>` or `c4-plan red-team plans/<plan-dir>`.
```

Add when relevant: the GitHub issue URL (`--github`), the `c4-project` suggestion if no project matched, and for `--parallel` which phases can run concurrently.
