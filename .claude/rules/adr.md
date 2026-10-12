# Architecture Decision Records

## When to write one
- Write an ADR for significant decisions that would be costly to reverse, or that someone would later ask "why was it done this way?" about.
- Examples: choosing a framework, library or external service; data model or storage choices; architectural patterns; integration approaches; security or authentication approaches.
- Routine changes, bug fixes and decisions that simply follow existing patterns don't need one.

## Planning
- If a task involves a decision that needs an ADR, list the ADR in the plan.
- Approving the plan, or working from an existing plan (e.g. a `PLAN.md`) that covers the decision, counts as accepting it. Write the ADR with status `Accepted`.
- If a decision that needs an ADR comes up during development and isn't covered by the plan, stop and get approval as for any other plan change.

## Where and how
- Put ADRs in `docs/adr/`, or in the project's existing ADR folder if it already has one.
- Number them in sequence with a short kebab-case title, e.g. `0003-use-redis-for-queues.md`.
- Keep them short: a page or less.
- Use this template:

```markdown
# ADR-NNNN: Title

- Date: DD/MM/YYYY
- Status: Accepted

## Context
The problem, and the constraints and forces at the time.

## Decision
What was decided.

## Consequences
The trade-offs: what becomes easier, what becomes harder, and any follow-up work.
```

## Changing a decision
- Never rewrite an accepted ADR. To change a decision, write a new ADR and set the old one's status to `Superseded by ADR-NNNN`.
- Fixing typos or broken links in an existing ADR is fine.

## Commits and summary
- Commit each ADR on its own, e.g. `docs(adr): record decision to use redis for queues`.
- Mention any new ADRs in the end-of-task summary.
