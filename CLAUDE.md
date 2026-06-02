# CLAUDE.md — maintaining this repo

A personal Claude Code skill marketplace. Each skill is an installable plugin under
`skills/<name>/` (manifest in `.claude-plugin/plugin.json`, registered in
`marketplace.json`); user-facing intro and install steps live in `README.md`. The notes
below are conventions for *editing* skills here that aren't obvious from the tree — they
deliberately don't restate the README or the global git rules in `~/.claude/CLAUDE.md`.

## Keep `SKILL.md` lean

`SKILL.md` is auto-loaded into context on every invocation, so long always-on prose
measurably degrades behavior (the cv-bullets dialog gate got under-executed once its
`SKILL.md` grew too long). Put bulky procedural detail — templates, widget mechanics,
long examples — into `references/*.md` that the workflow points to on demand, and keep
`SKILL.md` to the workflow skeleton. Runnable script commands in any of these files use
absolute `~/.claude/skills/<skill>/scripts/…` paths, because the working directory at
runtime is the user's project, not the skill folder.

## Versioning

SemVer, `0.x` until an interface settles. Each skill owns a `CHANGELOG.md`
([Keep a Changelog](https://keepachangelog.com/)). A version bump touches **three places**
that must stay in sync: `.claude-plugin/plugin.json` (`version`), the `Current version:`
footer in `SKILL.md`, and a new `CHANGELOG.md` entry.

## No personal data in skills

Paths and identity come from a git-ignored `config.md` (template: `config.md.example`);
never hard-code a CV path, name, or author pattern into a skill. The user's actual CV is
not in this repo.
