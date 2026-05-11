---
description: Create approved ticket worktrees from synced canonical clones
agent: build
---
Execute approved ticket setup for one Jira main issue in project `<jira-project-key>`.

Workflow:

1. Determine active ticket from current session or `tickets/<ISSUE>/PLAN.md`.
2. Determine target subtask for this execution:
   - prefer current session subtask context
   - otherwise ask user to choose one planned subtask/PR row
3. Read both `tickets/<ISSUE>/PLAN.md` and `tickets/<ISSUE>/subtasks/<SUBTASK-KEY>.md`.
4. Confirm ticket overview contains approved PR row for target subtask and detailed subtask file exists.
5. Refuse execution if target subtask plan is missing any of:
   - subtask key
   - repo
   - worktree path
   - branch name
   - PR title
   - proposed atomic commit plan
6. Run sync logic first for canonical source clones in `repos/`.
7. Ensure `tickets/<ISSUE>/worktrees/` exists.
8. Create git worktree from canonical source clone into planned worktree path for that one subtask.
9. Create branch using approved branch name from subtask plan.
10. Treat resulting worktree as owner of exactly one subtask and one PR.
11. For code changes inside prepared worktree, launch `patch-committer` and pass it:
    - target subtask key
    - worktree path
    - approved implementation scope from `tickets/<ISSUE>/subtasks/<SUBTASK-KEY>.md`
    - repo-local instruction files
    - planned atomic commits
    - required footer format when applicable
12. Have `patch-committer` implement approved subtask in that worktree, run smallest relevant checks first, then broader package checks as needed, and create planned commits.
13. After `patch-committer` completes, inspect resulting branch state, push branch, and create PR with `gh`, then convert PR to draft immediately.
14. Update `tickets/<ISSUE>/PLAN.md`, `tickets/<ISSUE>/subtasks/<SUBTASK-KEY>.md`, and `project.md` to reflect actual execution state, verification, push, and PR status.
15. Report implementation result, verification, commits, branch push, and PR URL.

Rules:

- Do not create worktrees until plan is approved or user clearly asks to proceed.
- Never implement ticket work in source clones under `repos/`.
- Worktrees must live under `tickets/<ISSUE>/worktrees/<repo>/`.
- Use `gh` CLI for GitHub access.
- Respect repo-local instruction rules once working inside each repo.
- If target worktree path already exists, inspect and ask before reusing or replacing it.
- Each worktree should correspond to one planned PR and one Jira subtask.
- All later commits in those worktrees must be drafted from planned `atomic-commit-drafter` commit plan first, then adjusted only if implementation scope changes.
- Tests that validate new behavior or fix must be committed with code they validate. Use separate `test(...)` commit only for independent coverage-only work.
- After any PR is created for worktree, convert it to draft immediately.
- Do not stop after setup only unless user explicitly says setup-only.
- Always adapt relevant markdown files during execution and after push/PR creation.
- Use `build` for ticket orchestration and `patch-committer` for worktree-local code edits, verification, and commit creation.
- If future env sync is added, run it after worktree creation and before implementation while keeping secret handling path-only.
