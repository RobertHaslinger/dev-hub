---
description: Plan ticket implementation and worktree strategy
agent: build
---
Plan implementation for one Jira main issue in project `<jira-project-key>`. Planning only. Do not create worktrees, branches, commits, PRs, or Jira subtasks yet.

Workflow:

1. Determine active ticket:
   - prefer ticket already established in current session or matching `tickets/<ISSUE>/PLAN.md`
   - otherwise use Jira MCP + `question` tool to let user select an assigned `<jira-project-key>` ticket
2. Ensure `tickets/<ISSUE>/PLAN.md` exists and `tickets/<ISSUE>/subtasks/` exists. Create missing structure if needed.
3. Read Jira issue details and current ticket overview `PLAN.md`.
4. Determine target subtask for this planning session:
   - if current session already clearly targets one subtask, use it
   - if exactly one active/planned subtask is relevant, use it
   - otherwise ask user which subtask to plan in detail
5. Use or create detailed subtask plan file at `tickets/<ISSUE>/subtasks/<SUBTASK-KEY>.md`.
6. Inspect only needed repo areas under canonical source clones in `repos/`.
7. Before finalizing plan, load and use `atomic-commit-drafter` plus repo-local commit guidance to draft proposed atomic commits for target subtask up front.
8. Plan in PR units. Default model is:
   - one Jira subtask per PR
   - one PR per worktree
   - one worktree per branch
9. Check whether suitable Jira subtasks already exist for main issue:
   - if they exist, map each planned PR to one subtask key
   - if they do not exist or are incomplete, propose exact subtasks needed and ask user whether to create them
10. Produce detailed implementation plan for target subtask with:
    - scope and assumptions
    - repo and package targets
    - dependency order
    - proposed atomic commit plan drafted up front
    - risks and open questions
    - validation plan
    - one worktree path
    - one branch name
    - one PR title
    - exact commit footer format for that subtask PR when repo requires one
11. Update ticket overview `tickets/<ISSUE>/PLAN.md` only with shared ticket-level data:
    - subtask list
    - PR overview row for target subtask
    - global decisions or open questions if newly discovered
12. Write detailed implementation notes into `tickets/<ISSUE>/subtasks/<SUBTASK-KEY>.md`.
13. End by asking user whether to refine subtask plan, create proposed Jira subtasks, or run `/execute-ticket` later.

Mandatory guidelines to reinforce in output and `PLAN.md`:

- Always work from canonical source clones in `repos/`, but never implement feature work there.
- Always create feature worktrees under `tickets/<ISSUE>/worktrees/<repo>/`.
- Always sync source clones to latest default branch before new worktree creation.
- Always use `gh` CLI for GitHub access.
- If editing inside cloned repos later, follow repo-local instruction files first.
- Default planning unit is one subtask per PR and one PR per worktree.
- `PLAN.md` must always include overview of resulting PRs.
- Ticket `PLAN.md` is ticket-level overview only. Detailed implementation notes belong in `subtasks/<SUBTASK-KEY>.md`.
- Do not overwrite one subtask's detailed plan with another subtask's implementation notes.
- Use exact repo rules already confirmed for this project, for example:
  - frontend: branch pattern `<frontend-branch-pattern>`, commit rules `<frontend-commit-rules>`, footer `<ticket-footer-format>`, PR title `<frontend-pr-title-format>`
  - backend: branch pattern `<backend-branch-pattern>`, commit rules `<backend-commit-rules>`, footer `<ticket-footer-format>`, PR title `<backend-pr-title-format>`

When writing ticket overview `PLAN.md`, include sections for:

- Jira summary
- scope
- subtasks
- PR overview
- global decisions
- global open questions
- follow-ups

`PR overview` must show one row per planned PR and include at least:

- subtask key
- repo
- worktree path
- branch name
- PR title
- dependency order
- status

When writing detailed subtask file `tickets/<ISSUE>/subtasks/<SUBTASK-KEY>.md`, include sections for:

- summary
- status
- repo
- worktree
- branch
- PR title
- commit and PR rules
- implementation plan
- validation plan
- open questions
- decisions
- session notes

Detailed subtask files must also include `proposed atomic commits` section drafted up front from `atomic-commit-drafter` guidance. That section must:

- list commits in planned order
- map each proposed commit to its files or file groups
- use repo-exact commit conventions already defined for project
