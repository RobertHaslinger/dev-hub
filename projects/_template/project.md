# Project Overview

## Purpose

Describe project, users, goals.

## Repos

| Repo | Purpose | Location | Notes |
| --- | --- | --- | --- |
| `<frontend-repo>` | UI app | `repos/<frontend-repo>/` | Canonical source clone. GitHub: `<github-owner>/<frontend-repo>`. Default branch: `<frontend-default-branch>`. |
| `<backend-repo>` | API/services | `repos/<backend-repo>/` | Canonical source clone. GitHub: `<github-owner>/<backend-repo>`. Default branch: `<backend-default-branch>`. |

## Active Worktrees

| Repo | Branch | Worktree Path | Purpose |
| --- | --- | --- | --- |

## Project Layout

```text
<project-name>/
  .opencode/
    commands/
    memory/
  project.md
  learnings.md
  tickets/
    <issue-key>/
      PLAN.md
      subtasks/
        <SUBTASK-KEY>.md
      worktrees/
        <frontend-repo>/
        <backend-repo>/
  repos/
    <frontend-repo>/
    <backend-repo>/
```

## Shared Commands

```bash
/sync-repos
/start-ticket
/implement-ticket
/execute-ticket
/clean-ticket
/open-worktree
/pr-feedback
```

## Constraints

- Jira project key: `<jira-project-key>`
- Use `gh` CLI for GitHub access.
- Canonical repo clones live under `repos/` and should stay on their default branches except for maintenance.
- Ticket implementation work must happen in `tickets/<issue-key>/worktrees/<repo>/`, not in `repos/` source clones.
- Never expose secrets from `.env`, `.npmrc`, or CI variables.
- Replace command and memory placeholders in `.opencode/` before relying on automation.
- Frontend branch pattern: `<frontend-branch-pattern>`.
- Frontend commit rules: `<frontend-commit-rules>`.
- Frontend PR title style: `<frontend-pr-title-format>`.
- Backend branch pattern: `<backend-branch-pattern>`.
- Backend commit rules: `<backend-commit-rules>`.
- Backend PR title style: `<backend-pr-title-format>`.
- Ticket footer format when required: `<ticket-footer-format>`.

## Decisions

- Treat this folder as project container, not single repo.
- Keep project-wide context here; keep repo-local code conventions in actual repos.
- Plan ticket work as one Jira subtask per PR and one PR per worktree.
- Keep ticket overview in `tickets/<ISSUE>/PLAN.md`, but put detailed implementation notes in `tickets/<ISSUE>/subtasks/<SUBTASK-KEY>.md`.
- Draft proposed atomic commits up front before implementation starts.
