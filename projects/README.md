# Projects

`projects/` holds root-level project containers for work coordinated from `dev-hub`.

Use one directory per product or client project.
Each project directory may contain:
- shared context and decisions
- cross-repo learnings
- references to active repos and worktrees
- multiple repos such as `frontend/`, `backend/`, `infra/`, `mobile/`

Suggested shape:

```text
projects/
  acme-app/
    project.md
    learnings.md
    repos/
      frontend/
      backend/
```

Rules:
- keep project-wide information at project root
- keep repo-specific code inside `repos/`
- store patterns, decisions, constraints, and useful commands in shared docs
- prefer worktrees inside repo directories when parallel feature streams needed

Start from `_template/` when creating new project container.
