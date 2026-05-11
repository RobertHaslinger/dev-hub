---
description: Sync canonical repo clones in repos/ to latest default branch
agent: build
---
Use `gh` CLI and git to prepare canonical source clones for ticket work.

Project paths:

- frontend source clone: `repos/<frontend-repo>`
- backend source clone: `repos/<backend-repo>`

Workflow:

1. Ensure both source clones exist. If missing, clone with `gh repo clone`:
   - `<github-owner>/<frontend-repo>` -> `repos/<frontend-repo>`
   - `<github-owner>/<backend-repo>` -> `repos/<backend-repo>`
2. For each source clone:
   - verify `origin` points to expected GitHub repo
   - fetch with prune
   - checkout configured default branch
   - pull tracked remote branch with `--ff-only`
3. Report current branch and HEAD SHA for each repo.

Rules:

- Use `gh` CLI for GitHub access.
- Source clones in `repos/` are canonical bases only. Do not implement ticket work there.
- Feature work must happen in ticket worktrees under `tickets/<ISSUE>/worktrees/<repo>/`.
- If source clone has unexpected local changes, stop and ask before modifying it.
