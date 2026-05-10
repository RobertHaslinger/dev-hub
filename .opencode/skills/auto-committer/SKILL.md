---
name: auto-committer
description: Wrap atomic-commit-drafter to draft, stage, and create atomic commits for the current git changes.
---

# Auto Committer

## Purpose

Use `atomic-commit-drafter` to produce an atomic commit plan for the current repository changes, then apply that plan by staging the appropriate files and creating the resulting commit(s).

## When to use

- After a user prompt results in code or file changes that should be committed locally.
- When the agent is instructed to automatically commit its just-completed changes.

## Workflow

1. Inspect the current git state with `git status -sb`, `git diff`, `git diff --staged`, `git diff --stat`, `git branch --show-current`, and recent commit bodies for the branch.
2. Load and use the `atomic-commit-drafter` skill to draft the smallest sensible atomic commit plan for the current changes.
3. If a single commit is proposed, stage only the files relevant to that commit and create it with the drafted message.
4. If multiple commits are proposed, stage and create each commit separately in the drafted order.
5. Run `git status` after the commit sequence to verify the result.
6. Recheck resulting commit size for each commit created in this run using `git show --name-only --pretty=format:` (or equivalent):
   - target is ~4 files max per non-refactor commit,
   - if any new commit exceeds ~4 files and is separable, immediately rewrite/split it before finishing,
   - if a >4-file commit is inseparable, record that rationale in the final report.

## Commit rules

- Follow the repo's conventional commit format and allowed scopes.
- Include the required `Refs: DPSEB-<ticket number>` footer when a ticket can be derived from the branch or otherwise determined.
- If recent related commits on the branch already use a consistent multi-ticket `Refs:` footer, reuse the same footer set unless the user specifies otherwise.
- Keep tests in the same commit as the change they validate.
- In this monorepo, keep each commit scoped to a single `packages/<name>` directory unless the change is inseparable; if inseparable, explain that in the commit plan.
- Separate formatting-only changes, refactors, dependency updates, and behavior changes when they are independently committable.
- Within a package, separate support-layer changes (for example services/compositions/models) from handler/route wiring when they can stand alone.
- Treat separate commands, skills, and instruction changes as separate commits when they can stand alone as different responsibilities.

## Safety

- Do not commit likely secrets such as `.env` files, credentials, or tokens.
- Do not include unrelated dirty files in the staged set.
- Do not use destructive git commands.
- If the ticket, scope, or grouping is unclear, stop and ask before committing.
- If the working tree contains unrelated user changes, commit only the files that belong to the current task.
