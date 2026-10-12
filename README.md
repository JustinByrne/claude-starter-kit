# Claude Starter Kit

A reusable set of rules, instructions and settings for [Claude Code](https://code.claude.com/docs), kept in one place so every new project starts with the same baseline.

Pull it into a fresh project, tweak anything project-specific, and commit the files as part of that project. The starter kit's own git history is **not** carried across.

## What's included

| Path                        | Purpose                                                                                                                          |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `CLAUDE.md`                 | Template for project-specific instructions (overview, commands, environments, git conventions, gotchas). Fill it in per project. |
| `.claude/rules/general.md`  | Plan, approve, develop workflow; staying on task; end-of-task summaries; UK English; comments and docs upkeep.                     |
| `.claude/rules/git.md`      | Branch safety, small atomic commits and `type(scope): summary` commit messages.                                                  |
| `.claude/rules/testing.md`  | TDD by default, test-first bug fixes, when to run tests, and never weakening tests to make them pass.                            |
| `.claude/rules/security.md` | Secrets, personal data, untrusted content, dependencies (including a 4-day minimum package age) and secure coding.               |
| `.claude/rules/adr.md`      | When to write Architecture Decision Records, where they go, a template, and superseding rather than rewriting them.              |
| `.claude/rules/php.md`      | PHP style: multi-line arrays and parameter lists with trailing commas, empty function bodies with `//`, no space after `!`, deferring to the project's formatter config. Only loads for `.php` files. |
| `.claude/settings.json`     | Turns off AI attribution lines on commits and PRs, pre-approves read-only git commands, and blocks Claude from reading `.env` files (other than `.env.example`). |

Claude Code loads `CLAUDE.md` and every file in `.claude/rules/` automatically at the start of each session. The exception is rules with `paths` frontmatter, such as `php.md`, which only load when Claude works with matching files.

> Adjust this table as the kit grows, so it always reflects what will land in a project.

## Adding the kit to a new project

The command below copies the **files only**. Nothing from this repository's `.git` directory is brought across, so the target project's history stays clean.

Run from the root of your project:

```bash
curl -fsSL https://github.com/JustinByrne/claude-starter-kit/archive/refs/heads/main.tar.gz \
  | tar -xz --strip-components=1 -k \
      --exclude='claude-starter-kit-main/README.md'
```

- `--strip-components=1` drops the `claude-starter-kit-main/` wrapper folder GitHub adds.
- `-k` (keep old files) stops `tar` from overwriting anything that already exists, such as an existing `CLAUDE.md`. Remove it if you do want to overwrite. On Linux, GNU `tar` prints `Cannot open: File exists` for each skipped file. That's expected, and the other files are still extracted.
- `--exclude` skips this README so it doesn't replace your project's own.

Works with both GNU `tar` (Linux) and `bsdtar` (macOS). The repository must be public, because an unauthenticated `curl` can't download from a private one.

## After pulling the kit in

1. Fill in `CLAUDE.md`. Run `/init` in Claude Code to draft it from the codebase, then review it, paying particular attention to the commands, environments and git sections. Delete the placeholder note at the top once it's complete.
2. If the project already had a `CLAUDE.md` or `.claude/settings.json`, `-k` will have skipped the kit's copy. Merge the kit's content in by hand, in particular the `attribution` and `permissions` blocks from `settings.json`.
3. Remove or adjust any rules in `.claude/rules/` that don't apply to the project.
4. Commit the files to the project's repository:

   ```bash
   git add CLAUDE.md .claude
   git commit -m "chore(claude): add claude code configuration from starter kit"
   ```

5. Keep personal, machine-specific overrides in `CLAUDE.local.md` and `.claude/settings.local.json`, and make sure both are in the project's `.gitignore`.

## Overriding the kit

Claude Code doesn't replace one instruction file with another: it loads them all into context together. If two files conflict, Claude may follow either one, so overrides need to be explicit.

| File | Applies to | Committed? |
| --- | --- | --- |
| `CLAUDE.local.md` in the project root | That project, for one person | No, add it to `.gitignore` |
| `~/.claude/CLAUDE.md` and `~/.claude/rules/` | Every project on one machine | No |
| The project's `CLAUDE.md` and `.claude/rules/` | That project, for everyone | Yes |

The kit's `CLAUDE.md` includes a **Rule priority** section telling Claude to follow `CLAUDE.local.md` first, then `CLAUDE.md`, then `.claude/rules/`. Keep that section when filling in the template. When overriding, name the rule being replaced:

```markdown
Override `.claude/rules/git.md`: committing directly to `main` is allowed in this project.
```

This is an instruction to Claude rather than something Claude Code enforces, so it's reliable but not guaranteed. To change a rule for everyone on a project, it's simpler to edit or delete the project's copy of the rule file directly.

Settings work differently. `.claude/settings.local.json` takes precedence over the project's `.claude/settings.json`, which takes precedence over `~/.claude/settings.json`, so single values such as `attribution` can be overridden locally. Permission lists are combined instead, and a `deny` rule always wins over an `allow`. To let Claude read a blocked `.env` file, remove the rule from the project's `settings.json`.

## Pulling in updates later

Because the kit is copied rather than linked, projects don't pick up changes automatically. To refresh a project, re-run the command **without** the `-k` flag and with `CLAUDE.md` excluded, so the project's filled-in copy isn't replaced by the template:

```bash
curl -fsSL https://github.com/JustinByrne/claude-starter-kit/archive/refs/heads/main.tar.gz \
  | tar -xz --strip-components=1 \
      --exclude='claude-starter-kit-main/README.md' \
      --exclude='claude-starter-kit-main/CLAUDE.md'
```

Then review the changes with `git diff` before committing, so you don't lose any project-specific edits to the rules or `settings.json`.

## Maintaining the kit

- Keep rules generic: anything specific to a single project belongs in that project's `CLAUDE.md`, not here.
- Prefer several small, focused files in `.claude/rules/` over one long `CLAUDE.md`.
- Tag releases (e.g. `v1.0.0`) so projects can pin to a known version. To install a tag, swap `refs/heads/main` for `refs/tags/v1.0.0` in the URL, and change the `--exclude` paths to start with `claude-starter-kit-1.0.0/` (GitHub drops the leading `v` from the folder name).
- This repository is public. Never commit secrets, tokens, client data or organisation-specific policy to it.
