---
description: Fetch PR feedback and render interactive one-shot decision prompt
agent: build
subtask: false
---

You are preparing one-shot PR feedback intake for user.

PR reference from user:
$ARGUMENTS

Goal:
- Fetch review feedback for target GitHub pull request.
- Render concise markdown table.
- Then always show interactive prompt so user can choose `do`, `won't do`, or `skip` for each item in one pass.
- Stop after presenting table and interactive prompt.
- Do not implement code changes yet.
- Do not post replies yet.

Instructions:
1. Determine target PR.
- If `$ARGUMENTS` contains GitHub PR URL, use it.
- If `$ARGUMENTS` contains owner/repo#number or PR number, resolve it from current repo.
- If `$ARGUMENTS` is empty, infer current repo from git and ask `gh` for PR associated with current branch.
- If still cannot determine PR, ask one targeted question and stop.

2. Fetch feedback with `gh`.
- Prefer unresolved review comments / threads and open review feedback over generic issue comments.
- Include enough context to let user decide in one pass:
  - stable row id
  - reviewer
  - file path and line when present
  - short summary of comment
  - whether it already looks outdated/resolved if available
- Ignore bot noise where reasonable.

3. Render decision table in markdown.
- Keep it compact and scannable.
- Use columns:
  - `ID`
  - `Reviewer`
  - `Location`
  - `Summary`
  - `Suggested Action`
- `Suggested Action` must be one of:
  - `do`
  - `won't do`
  - `skip`
- Default to best suggested action based on comment.

4. After table, always render interactive prompt.
- Use question tool with one row per feedback item.
- Keep prompt labels stable by row id so answers map back cleanly.
- Choices must be `do`, `won't do`, `skip`.
- Put recommended action first.
- If `won't do` decision likely needs PR reply, ask for exact reply text after selection if not already provided.

5. Stop after presenting table and interactive prompt.
- Do not begin implementation.
- Do not create commits.
- Do not update instruction files.

6. Best next step.
- Mention briefly that best next step after choices are captured is to implement approved `do` items and post replies for `won't do` items with provided text.
- For approved items that get implemented later, reply on tackled comments with exact format `tackled in <commit>`.

7. Durable learning step.
- If implemented PR feedback reveals reusable workflow or coding lesson, update smallest relevant project instruction/command and persist that lesson in project memory after implementation so future runs benefit automatically.

Output requirements:
- Start with resolved PR reference.
- Then show markdown table.
- Then show interactive prompt using question tool.
- Keep whole response concise.
