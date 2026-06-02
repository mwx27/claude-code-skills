# Changelog

All notable changes to the `cv-bullets` skill are documented here.

Format based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/). As an early-stage skill, it stays in the `0.x` range — behavior may change between minor releases until the interface settles and a `1.0.0` is cut.

---

## [0.1.0] — 2026-06-02

First public release on the marketplace. This entry describes the feature set the skill ships with, not a delta from earlier work (prior iterations were never publicly released — see *Prior history* below).

### Features

- **Three modes** — `full` (default: read repo + git log + dialog + generate + write), `refinement` (polish existing bullets without scanning the repo), `from-memory` (structured interview for projects without repo access).
- **Mandatory Phase 0 dialog gate** — captures what automated analysis can't: related repositories, target CV section, new-entry-vs-refinement, the flagship claim, limits, and CV style strategy (mirror vs. canonical rules).
- **Multi-repo discovery** (`scripts/scan_siblings.py`) — scans sibling directories for git repos the user contributed to and offers them via a multi-select widget, so cross-repo work isn't lost.
- **Git + PR metrics** (`scripts/analyze_git.py`) — conventional-commit breakdown, feat:fix ratio, quality ratio (refactor+test+perf), test-touch %, average commit size, active days, and PR counts authored by the user via `gh` (silent skip when `gh` is unavailable).
- **Baseline-vs-senior categorization** — every achievement is labelled BASELINE / SOLID / SENIOR / FLAGSHIP (`references/BASELINE_VS_SENIOR.md`) so only above-the-bar signals become bullets.
- **Bilingual composition (Polish + English)** following a strict style guide (`references/STYLE_GUIDE.md`): Polish noun-forms, English action verbs, term-of-art kept in English, numbers over adjectives, no calques.
- **Length & count discipline** — max 5 bullets (never padded to hit a number), 105-char ceiling, with one optional extended slot up to 170 chars per section for a dense signal that would weaken if split.
- **TechStack reconciliation** — proposes an updated `techStack` field from the composed bullets and repo dependencies; keeps the existing one if already strong.
- **Comparison gate + duplicate detection** — when refining/replacing, judges new vs. old bullets per item (NEW BETTER / OLD BETTER / TIE / NEW TOPIC) and flags bullets that resemble entries in other projects.
- **Inventory output** — a categorized markdown inventory saved under `<cv_path>/content/data-inventories/`, with chosen items marked ⭐, for offline review and interview prep.
- **Write-first flow** — writes directly to `cv.pl.ts` / `cv.en.ts`, leaves changes unstaged, and points to `git diff` as the review surface (no chat-approval gate).
- **Per-user configuration** (`config.md`) — `cv_path` and `git_author_pattern` are read from `~/.claude/skills/cv-bullets/config.md`; the skill prompts for them and offers to create the file on first run if it's missing. No personal paths or identity are baked into the skill.

### Known limitations

- The Phase 0 dialog gate can still be under-executed on long runs; not yet confirmed by an eval harness.
- `scripts/scan_siblings.py` does not deduplicate snapshot/copy directories (e.g. `repo`, `repo-copy`, `repo-copy 2` are counted as separate repos).
- No automated eval harness yet — behavior is validated by walkthrough only.

---

## Prior history (pre-publication)

Before this release the skill went through roughly ten private iterations (internally numbered v1–v10); none were ever publicly released, and that `vN` numbering is retired. In brief, it evolved as follows:

- **Early versions** established the core bilingual Polish/English bullet rules and the style guide.
- **Mid versions** added multi-repo discovery, git metrics, the baseline-vs-senior categorization reference, the `from-memory` mode, and the CV-style strategy question.
- **Later versions** dropped the chat-approval gate in favor of the write-first flow (with `git diff` as the safety net), and treated bullet length and count as ceilings rather than targets.
- **The final pre-publication version** added PR statistics, TechStack reconciliation, and the comparison + cross-project duplicate gates.

`0.1.0` is the consolidation of that work into an installable, configurable marketplace plugin.
