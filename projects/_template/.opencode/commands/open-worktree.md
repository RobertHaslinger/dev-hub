---
description: Select local ticket worktree and open it in IntelliJ IDEA
agent: build
---
Open one existing local ticket worktree in IntelliJ IDEA.

Workflow:

1. Inspect local worktrees under `tickets/*/worktrees/*` and prefer leaf worktree folders under `tickets/*/worktrees/*/*` when they exist.
2. If current session already points at ticket and matching worktrees exist, prioritize those options first.
3. Present selectable options with `question` tool using labels like `<ISSUE> / <repo> / <worktree>` for leaf worktrees, or `<ISSUE> / <repo>` only when no deeper worktree folder exists.
4. After user selects worktree, verify path exists.
5. Launch IntelliJ IDEA for that worktree using:
   - `"/Applications/IntelliJ IDEA.app/Contents/MacOS/idea" "<worktree-path>"`
6. Report which path was opened.

Rules:

- Only open existing local worktrees under `tickets/<ISSUE>/worktrees/<repo>/`, and when repo folder contains sub-worktrees, open selected sub-worktree folder rather than parent repo folder.
- If no worktrees exist, stop and tell user to run `/execute-ticket` first.
- If IntelliJ IDEA launcher path is missing, stop and report that clearly.
- Do not create, modify, or remove worktrees in this command.
