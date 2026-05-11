---
description: Select assigned Jira ticket and start ticket workspace
agent: build
model: lmstudio/google/gemma-4-e4b
subtask: true
---
Use Jira MCP to start work for one assigned main Jira issue in project `EAC`.

Workflow:

1. Confirm current Atlassian user with Jira MCP.
2. Load Jira issues assigned to Robert Haslinger in project `EAC` that are not done.
3. Present selectable options to user with `question` tool. Each option should include issue key and short summary.
4. After user selects issue, fetch full Jira issue details.
5. Ensure ticket directory exists at `tickets/<ISSUE-KEY>/` in this project container.
6. Ensure subtask planning directory exists at `tickets/<ISSUE-KEY>/subtasks/`.
7. Create or update ticket overview file `tickets/<ISSUE-KEY>/PLAN.md` with shared ticket-level sections only:
   - title and Jira link
   - status and assignee
   - summary
   - scope
   - subtasks
   - PR overview
   - global decisions
   - global open questions
   - follow-ups
   - session notes
8. Do not write detailed implementation notes for one specific subtask into ticket overview file. Those belong in `tickets/<ISSUE-KEY>/subtasks/EAC-<sub>.md`.
9. Keep `PLAN.md` as running source of truth for ticket-wide planning and PR overview in later turns.

Rules:

- This project means `/Users/roberthaslinger/PERSONAL/dev-hub/projects/opencode-demo`.
- Use Jira MCP for Jira access.
- Use `gh` CLI for any GitHub access if GitHub work becomes necessary.
- Canonical source clones live in `repos/` and must remain base clones, not feature workspaces.
- Ticket feature worktrees belong under `tickets/<ISSUE-KEY>/worktrees/<repo>/`.
- `PLAN.md` must always include PR overview section, even before subtasks exist.
- Detailed implementation notes must live in per-subtask files under `tickets/<ISSUE-KEY>/subtasks/`.
- Treat selected ticket as main issue level unless user says otherwise.
- If `PLAN.md` already exists, preserve useful notes and update in place.
- After setup, report selected ticket and `PLAN.md` path.
