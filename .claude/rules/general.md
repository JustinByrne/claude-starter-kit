# General

## Workflow
- Work in three stages: plan, approve, develop.
- Before starting any non-trivial work, present a short plan: what will change, which files are affected, and how it will be tested. Wait for approval before making changes.
- Trivial changes (e.g. a typo or a one-line fix the user has described exactly) and questions that don't change code don't need a plan.
- If the plan needs to change during development, stop and get approval for the new plan.
- If requirements are unclear, ask rather than guess.

## Scope
- Stay strictly within the task. No unrelated refactors, fixes or "while I was here" changes.
- If you notice anything else worth fixing, mention it in the summary instead.
- Follow the codebase's existing patterns before introducing new ones.
- Do not leave dead code, commented-out code or stray TODOs.

## Summary
- Always end a task with a summary covering what changed, what was tested, and anything not checked or still outstanding.

## Language
- Use UK English in comments, docs, commit messages and responses.
- For code identifiers, follow the existing codebase and framework (e.g. keep `color` if the project or framework already uses it).

## Comments and docs
- Comments explain why, not what.
- Do not add comments to code you aren't otherwise changing.
- When behaviour changes, update the related docs (e.g. the README, `CLAUDE.md` or API docs) in the same piece of work.
