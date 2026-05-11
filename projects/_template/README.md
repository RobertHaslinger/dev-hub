# Project Template

Copy this directory to `projects/<project-name>/`.

Purpose:
- group multiple repos under one project root
- keep shared context near repos
- retain learnings across parallel feature work
- ship reusable OpenCode workflow commands with project container

Suggested setup:

```text
<project-name>/
  .opencode/
    commands/
    memory/
  project.md
  learnings.md
  repos/
    <frontend-repo>/
    <backend-repo>/
```

Use `project.md` for current project shape, active repos, commands, constraints.
Use `learnings.md` for discoveries worth reusing later.

## Fill placeholders first

Replace these placeholders before use:

- `<project-name>`
- `<project-root-abs-path>`
- `<jira-project-key>`
- `<jira-assignee-name>`
- `<github-owner>`
- `<frontend-repo>`
- `<backend-repo>`
- `<frontend-default-branch>`
- `<backend-default-branch>`
- `<frontend-branch-pattern>`
- `<backend-branch-pattern>`
- `<frontend-commit-rules>`
- `<backend-commit-rules>`
- `<frontend-commit-conventions>`
- `<backend-commit-conventions>`
- `<frontend-pr-title-format>`
- `<backend-pr-title-format>`
- `<ticket-footer-format>`

After replacement, review `.opencode/commands/` and `project.md` for any project-specific workflow tweaks.
