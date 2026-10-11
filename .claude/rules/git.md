# Git

## Branches and safety
- Never commit directly to `main` or `master`. Create a branch first, named `type/short-description` (e.g. `fix/quote-due-date`), using the commit message types.
- Do not push or open pull requests unless asked.
- Ask before running anything that can discard work: `git reset --hard`, `git clean`, `git checkout -- <path>`, `git restore`, `git stash drop`, `git branch -D` and `git push --force`.
- If a force push is needed, use `--force-with-lease`, and only on your own branch.
- Do not rewrite commits that have already been pushed (`git commit --amend`, rebase) without asking.
- If a pre-commit hook fails, fix the problem, re-stage and make a new commit. Do not use `--amend`: the failed commit never happened, so amending would change the previous commit.
- Never commit secrets, `.env` files or credentials. Check the diff before committing, and stop and flag anything that looks like one.
- Only commit changes made as part of the current task. Leave other uncommitted changes unstaged and mention them.
- Do not change git config (user name, email, hooks and so on).

## Commits
- Never make one large commit. Split work into small, logical, atomic commits.
- Each commit covers one concern (e.g. refactor, feature, tests, docs, config), not a mix.
- Commit completed work without asking for approval. Do not push or open pull requests unless asked.
- Before committing, run `git status` and `git diff`, then plan the commit sequence and list it. You do not need approval: list the plan, then make the commits.
- Stage selectively with `git add <paths>`. Never use `git add -A`, `git add .` or `git commit -a`.
- Run `git add` and `git commit` as separate commands.
- Limits: at most 10 files and 300 changed lines per commit.
- The limits may be exceeded only when a single logical change cannot sensibly be split (e.g. lockfiles, generated files, bulk renames). Never split a change artificially just to fit, and mention in the commit plan when a commit exceeds them.
- Never use `--no-verify`.
- Each commit must leave the project building and its tests passing. Exception: when following TDD, a commit may add failing tests ahead of the commit that makes them pass.
- Order commits so each is easy to review: refactors come before the feature that depends on them.

## Commit messages
- Format: `type(scope): summary`, e.g. `fix(tasks): bring quote circulation due date forward`.
- Use standard types: `feat`, `fix`, `refactor`, `test`, `docs`, `chore`, `perf`, `style`, `build`, `ci`.
- Write the summary in the imperative mood ("add", not "added"), lowercase, with no trailing full stop, and keep the whole first line to 72 characters or fewer.
- Add a body explaining why the change was made when that isn't obvious from the diff.
- Mark breaking changes with `!` after the type or scope (e.g. `feat(api)!: remove v1 endpoints`) or a `BREAKING CHANGE:` footer.
- When there is a ticket reference (e.g. a Jira key), include it in a footer, e.g. `Refs: ABC-123`.
- Do not add a `Co-Authored-By:` trailer or any other AI attribution line to commit messages.
