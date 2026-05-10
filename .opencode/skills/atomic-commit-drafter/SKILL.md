---
name: atomic-commit-drafter
description: Draft atomic conventional commit messages from the current git changes. Use to propose commit splits or a single commit message before any staging/committing.
---

# Atomic Commit Drafter

## Purpose

Draft a set of atomic conventional commits from the repository's current changes without staging, committing, or modifying files.

## When to use

- The user asks for commit messages, commit splitting, or to commit changes.
- The user requests a changelog-ready conventional commit message.

## Inputs to inspect

- `git status -sb`
- `git diff` and `git diff --staged`
- `git diff --stat`
- `git branch --show-current`

Extract a Jira-style ticket key from the branch name when present (example: `DPSEB-123`). Also inspect recent related commits on the branch for an established `Refs:` footer set and preserve it when drafting follow-up commits for the same task.

## Rules for atomicity

- One intent per commit.
- Keep tests with the change they validate.
- Separate dependency/version bumps from code changes. One commit per package if multiple.
- In this monorepo, do not mix files from different `packages/<name>` directories in the same commit unless the change is inseparable; if inseparable, call that out explicitly in the plan.
- Separate formatting-only changes from behavior changes.
- Separate refactors from functional changes.
- Within one package, keep support-layer changes (for example services/compositions/models) separate from handler/route wiring when they are independently committable.
- Separate commands, skills, and instruction updates when they are independently useful and do not need to land together.
- If a single file mixes unrelated edits, call out the need for partial staging.
- Prefer small commits; split when a non-refactor commit exceeds ~4 files unless inseparable.

## Conventional commit guidance

- Types: `feat`, `fix`, `refactor`, `docs`, `test`, `build`, `ci`, `style`.
- Scope: module/package/subsystem; ask if unclear.
- Dependency-only: `build(<scope>): update dependency `<package>``.
- If breaking: add `!` and a `BREAKING CHANGE:` footer.

## Output format

Provide a numbered list of proposed commits. For each commit include:
- Draft commit message.
- Planned file list (or concise file groups) and an estimated file count.
- If estimated file count is greater than ~4, include an explicit inseparable rationale; otherwise split further.

Example:

1) Message:
   ```
   build(auth): add eslint config and scripts

   Refs: DPSEB-123
   ```

## Footers

- Always include `Refs: <ticket>` when a branch-derived key exists.
- Use the same `Refs:` footer across related commits for a single task.
- If recent commits for the same branch task already use multiple `Refs:` values, reuse that exact footer set unless the user requests a change.

## Ask for missing context

- If scope, ticket, or grouping is unclear, ask before finalizing.
- If no ticket reference exists, ask for the expected reference.

## Safety

- Do not stage, commit, or modify files while drafting, unless explicitly requested by the user or agent workflow.
- If the working tree is clean, say so and ask for the target changes or a patch.
