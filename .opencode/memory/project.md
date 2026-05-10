---
description: 'Stores durable, high-signal information about this codebase: commands, architecture notes, conventions, and gotchas.'
label: project
limit: 5000
read_only: false
---
Workspace `/Users/roberthaslinger/PERSONAL/dev-hub` now contains former global Opencode config moved from `~/.config/opencode`. Key files at repo root: `AGENTS.md`, `agent-memory.json`, `opencode.json`, `journal/`, `memory/`, `plugins/`, `package.json`, `package-lock.json`, `node_modules/`, and `projects/`. Local Opencode runtime state remains under `.opencode/`.

Project purpose: `dev-hub` is entry point for software development work. Use it to connect to many separate projects and parallel feature streams. Prefer git worktrees for project isolation and concurrent work. Treat `dev-hub` itself as evolving product with its own features, separate from connected project worktrees.

Working convention: preserve `dev-hub` as control center for many projects, favor workflows/docs/tooling that make switching between projects and worktrees fast, and distinguish clearly between changes for `dev-hub` itself versus changes for connected project worktrees.

Projects convention: use `projects/` for root-level project containers. Each project directory can group multiple repos under `repos/` (for example `frontend/` and `backend/`) while keeping shared project context and cross-repo learnings in root files like `project.md` and `learnings.md`.

Proactive guidance: watch for repeated workflow patterns, friction, and manual steps. Suggest useful, efficient `dev-hub` features whenever patterns appear that could make future development easier. Surface those suggestions proactively at any time once identified.
