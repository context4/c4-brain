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
Implement the plan phase by phase, starting with phase 1: read `plan.md` and the phase file, do its steps, run its Verification, tick its checkboxes, then move on.
Optional before that: `c4:plan validate plans/<plan-dir>` or `c4:plan red-team plans/<plan-dir>`.
```

Add when relevant: the GitHub issue URL (`--github`), the `c4:project` suggestion if no project matched, and for `--parallel` which phases can run concurrently.
