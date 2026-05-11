---
description: Durable project conventions, layout, workflows, and constraints for <project-name> container.
label: project
limit: 5000
read_only: false
---
Project container, not single app repo. Shared docs live here; repo-specific code stays in actual repos.

Repos:
- `<frontend-repo>` canonical clone at `<project-root-abs-path>/repos/<frontend-repo>` (GitHub `<github-owner>/<frontend-repo>`)
- `<backend-repo>` canonical clone at `<project-root-abs-path>/repos/<backend-repo>` (GitHub `<github-owner>/<backend-repo>`)

Rules:
- Use `gh` CLI for GitHub access and repo operations in this project.
- Update `project.md` when repo layout, commands, constraints, or worktrees change.
- Update `learnings.md` for durable cross-repo discoveries.
- If editing inside project repos, follow repo-local instruction files first.
- For Jira main issue work, create `tickets/<ISSUE>/PLAN.md` in this container at start and keep it updated with scope, PR overview, global decisions, constraints, validation summary, and follow-ups.
- Detailed subtask implementation notes live in `tickets/<ISSUE>/subtasks/<SUBTASK-KEY>.md`.
- `/implement-ticket` must draft proposed atomic commits up front with `atomic-commit-drafter` and record them in subtask plan.
- After any PR creation in this project, convert PR to draft immediately.
- For PR feedback in this project, first collect decisions with interactive prompt, then implement approved items, reply on tackled comments with `tackled in <commit>`, post replies for declined items, and persist reusable learnings into project memory/instructions.
- Canonical source clones live under `repos/` and should be synced to latest default branch before creating ticket worktrees.
- Every new worktree should install project dependencies before work begins when repo tooling requires it.
- Never implement ticket work directly in `repos/` canonical clones; use `tickets/<ISSUE>/worktrees/<repo>/`.
- When opening ticket worktrees in tools like IntelliJ, prefer leaf worktree folders under `tickets/<ISSUE>/worktrees/<repo>/<subworktree>` when present, not parent repo-level directory.
- If env sync later added, keep it path-only and never read, print, diff, summarize, or commit secret contents.

Quick facts:
- Jira project key: `<jira-project-key>`.
- Workflow commands: `/sync-repos`, `/start-ticket`, `/implement-ticket`, `/execute-ticket`, `/clean-ticket`, `/open-worktree`, `/pr-feedback`.
- `<frontend-repo>`: repo under `<github-owner>`, default branch `<frontend-default-branch>`, conventions `<frontend-commit-conventions>`, branch pattern `<frontend-branch-pattern>`, required footer `<ticket-footer-format>` for ticket work.
- `<backend-repo>`: repo under `<github-owner>`, default branch `<backend-default-branch>`, conventions `<backend-commit-conventions>`, branch pattern `<backend-branch-pattern>`, required footer `<ticket-footer-format>` for ticket work.
