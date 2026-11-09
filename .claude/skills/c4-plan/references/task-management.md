# Task List Mirroring

Plan files are the durable source of truth. A runtime task list (a todo or task tool, if the agent has one) is an optional, session-scoped view.

## When

After writing a plan with at least three meaningful phases, unless `--no-tasks` or the plan is too small to benefit. If the runtime has no task-list tool, skip and keep status in the plan files. Do not infer support from the client's name; check the tools actually available.

## Mirroring

1. Read `plan.md` and every phase file; checked boxes are done, unchecked are remaining.
2. Create one item per phase (or per high-risk step) as an imperative action, in dependency order, each naming its phase file.

## Sync-back

When work happens against the plan:
1. Update checkboxes and phase `status` in the files, sweeping every phase, not only the active one.
2. Update the phases table and `plan.md` status from the real checkbox state.
3. When states disagree, the plan files win. Report any item that cannot be mapped back before claiming completion.
