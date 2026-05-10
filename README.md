# dev-hub

Hub repo for shared development workflow, Opencode config, templates, and project scaffolding.

## What root repo tracks

- root workflow/config files such as `AGENTS.md`, `opencode.json`, `agent-memory.json`
- shared `.opencode/` config and skills
- `projects/README.md`
- `projects/_template/` project scaffold
- `projects/.opencode/` shared project-structure config

## What root repo ignores

- real project folders under `projects/`
- nested repos and worktrees inside real project folders
- dependency/runtime folders such as `node_modules/`
- local editor noise such as `.idea/`

## Rule

Use `dev-hub` repo for hub evolution.
Use nested project repos for actual product code.
