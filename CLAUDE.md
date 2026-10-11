# Project

<!-- Run /init to have Claude draft these sections from the codebase, then review them. Delete any section that doesn't apply. -->

> If this file still contains placeholder text (`...` or the descriptions below), it hasn't been filled in yet. Do not treat placeholders as real project details: offer to fill them in by exploring the codebase. Delete this note once the file is complete.

## Overview
What the project does and who uses it.

## Tech stack
Languages, frameworks and key libraries.

## Commands
- Install: `...`
- Build: `...`
- Dev server: `...`
- Test (full suite): `...`
- Test (single test): `...`
- Lint: `...`
- Format: `...`
- Migrations: `...`
- Audit: `...`

## Architecture
Main directories and how they fit together.

## Conventions
Coding style, naming, where new files go, and patterns to follow or avoid (e.g. "Use form requests for validation, not controller logic").

## Environments
| Environment                        | Claude may use it? | Notes                            |
| ---------------------------------- | ------------------ | -------------------------------- |
| Local                              | Yes                | ...                              |
| Test                               | Yes                | How the test database is set up. |
| Staging, sandbox, demo, production | No                 |                                  |

## Git
- Main branch: `...`
- Commit scopes: `...`
- Ticket key prefix: `...` (e.g. `ABC-`, used in the `Refs:` footer)

## Gotchas
Non-obvious things that trip people up: flaky services, legacy areas not to touch, required setup steps.

## Project-specific rules
Anything that applies only to this project. Shared rules live in `.claude/rules/`.

## Rule priority
If instructions conflict, follow them in this order:
1. `CLAUDE.local.md` (personal, not committed)
2. This file
3. `.claude/rules/`

Overrides should name the rule they replace, e.g. "Override `.claude/rules/git.md`: committing directly to `main` is allowed in this project."
