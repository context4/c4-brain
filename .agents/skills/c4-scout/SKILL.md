---
name: c4-scout
description: "Fast read-only discovery of the files that matter for a task — in this brain (index.md, wiki/, projects/, plans/, raw/) or in a code repository. Returns a short, ranked file map with one line on why each file matters. Use before planning, implementing, or answering a question that needs repository context. Invoke to find where something lives, gather context for a task, or orient in an unfamiliar folder."
license: MIT
metadata:
  author: c4-brain
  version: "1.0.0"
---

# Scout (`c4-scout`)

Find the smallest set of files a task actually needs, fast, without changing anything. Answer in the user's language.

## Rules

- **Read-only.** Never edit, move, or create files while scouting (the optional report in step 5 is the only exception).
- **Narrow before reading.** List and search first; open a file only when its name or a search hit says it is relevant. Read large files by section, not whole.
- **Skip noise:** `.git/`, `node_modules/`, build output, caches, lockfiles, binaries, media in `raw/videos` and `raw/images` (look at names only), `.env*` and anything that looks like a secret — never open those.
- **Evidence, not guesses.** Every file in the result is something you actually saw. If you did not find it, say so.

## Procedure

1. **Frame the target.** Restate in one line what you are looking for and where (default: the current working directory). Pick 3–6 search terms: names, synonyms, likely file names, in both Russian and English when the content may be in either.
2. **Start from the maps.**
   - In this brain: read `index.md` first, then `projects/*/project.yaml` and the `plan.md` frontmatter in `plans/` and `projects/*/plans/`. With a current project, start inside `projects/<slug>/` (its `project.yaml → wiki` lists the relevant wiki pages). These maps usually point straight at the right files.
   - In a code repo: read the root README, the agent instructions (`CLAUDE.md` / `AGENTS.md`), and the manifest (`package.json`, `pyproject.toml`, `go.mod`, …) to learn the layout.
3. **Search.** Use file-name globbing and content search with the terms from step 1. In the brain also follow `[[wiki-links]]` and the `sources:` / `projects:` frontmatter of the pages you open. In code, follow imports and call sites one hop from each hit.
4. **Fan out only when it is big.** If the area is large and the runtime offers subagents, split by directory (one subagent per top-level area, each told to stay read-only and return paths with one-line reasons). Otherwise keep going sequentially. Stop once new searches stop producing new relevant files.
5. **Report.**

```markdown
### Found: <target>
1. `path/to/file` — why it matters (one line)
2. `path/to/other` — ...

### Related but secondary
- `path` — ...

### Not found / gaps
- <what you looked for and did not find, and where you looked>
```

Rank by relevance, keep it under ~20 entries. If the user or a calling skill asks for a saved report, write it to the active plan's `reports/` folder (`<plan-dir>/reports/scout-<slug>.md`); otherwise keep it in the chat.

## Used by

- `c4-plan` — scouting before and during planning.
- `c4-cook` — a quick pass right before each phase to confirm paths are still right.
- Brain operations (ingest, query, lint) — finding the pages a new source touches.
