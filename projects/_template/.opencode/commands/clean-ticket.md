---
description: Remove finished ticket folder and local worktrees safely
agent: build
---
Clean one finished Jira ticket from local machine only.

Goal:

- remove local worktrees under `tickets/<ISSUE>/worktrees/`
- remove `tickets/<ISSUE>/PLAN.md`
- remove whole `tickets/<ISSUE>/` directory
- keep canonical source clones in `repos/` intact

Workflow:

1. Determine target ticket:
   - prefer active ticket from current session or matching `tickets/<ISSUE>/PLAN.md`
   - otherwise inspect local `tickets/` directories and use `question` tool to let user choose one
2. Inspect ticket directory:
   - read `tickets/<ISSUE>/PLAN.md` if present
   - inspect `tickets/<ISSUE>/worktrees/`
   - cross-check worktrees against canonical source clones in `repos/`
3. Safety checks for each discovered worktree:
   - inspect git status for uncommitted changes
   - inspect whether branch is ahead of remote or has no upstream
   - inspect whether worktree path exists but is stale or unregistered
4. If any worktree has uncommitted changes, unpushed commits, missing upstream, or other risky state, stop and ask for explicit confirmation before destructive cleanup.
5. If safe or user explicitly confirms after warning:
   - remove each registered worktree using `git worktree remove`
   - prune stale worktree metadata from canonical clones if needed
   - remove remaining files under `tickets/<ISSUE>/`
   - remove whole `tickets/<ISSUE>/` directory
   - update `project.md` active worktrees table
6. Report removed worktrees and final cleanup result.

Rules:

- Local cleanup only. Do not delete remote branches or change GitHub state.
- Never delete canonical source clones under `repos/`.
- Never delete without warning when risky state exists.
- Use `gh` CLI only if GitHub inspection somehow becomes necessary; default cleanup should stay local.
- If target ticket folder contains unexpected extra files, mention them before deletion.
