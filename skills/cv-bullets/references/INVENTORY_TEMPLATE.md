# Inventory File — template & conventions

The skill persists the categorized inventory as a markdown file the user reviews
offline, uses for interview prep, and compares against future iterations.

**The inventory is a truth document, not a journey log.** Only include items that survive
verification (Phase 2.5 authorship gate, Phase 4 categorization). Items rejected during the
blame check are *not* documented here — no "considered but cut" or audit-trail section. The
user must be able to trust every row as verifiably theirs.

## When & where

- **Path**: `<cv_path>/content/data-inventories/{project-slug}-{YYYY-MM-DD}.md`
  (slug: lowercase, dashes for spaces — `mobile-app`, `web-dashboard`). If the CV dir is
  elsewhere due to sandbox limits, use the parent of wherever the CV files were found.
- **Always versioned by date** — never overwrite. If today's file already exists for
  this project, append `-2`, `-3`, …
- Create `data-inventories/` if it doesn't exist.
- **Skip entirely in `refinement` mode** — there's no fresh inventory to save.
- **Write after Phase 6.6** (composition + all reviews complete), then update in Phase 8
  if the user iterates.

## Population order

- "Repo metrics" — after Phase 2 (git data), augmented with PR data if `gh` available.
- "Inventory table" categories — after Phase 4.
- "Chosen for CV" + ⭐ markers — after Phase 5.
- "TechStack revision" — after Phase 6.5.
- "Duplicate warnings" — after Phase 6.6 Part B, only if duplicates exist (else omit).

## Template

```markdown
# CV Inventory: {Project Name}

**Date**: {YYYY-MM-DD}
**Repos analyzed**: {comma-separated list, with paths}
**Total commits found**: {N user / M total}
**Active period**: {start_date} – {end_date}

## Inventory table

{Single table sorted by category (FLAGSHIP first, then SENIOR, SOLID, BASELINE).
Items chosen for the final CV are marked ⭐ in the Status column.}

| Status | Item | Source | Category | Evidence |
|--------|------|--------|----------|----------|
| ⭐ | Custom AI SDK v6 transport with streaming | mobile-app | FLAGSHIP | src/ai/transport.ts, 12 commits in 11.2025 |
| ⭐ | Cross-repo auth migration (header → cookie) | mobile-app, mobile-app-backend | FLAGSHIP | auth refactor across ~12 endpoint groups |
| ⭐ | RN↔WebView bridge with Clerk handoff | mobile-app, mobile-app-funnels | SENIOR | bridge in src/webview/, Clerk ticket passing |
|   | Sentry session replay + PostHog ~80 events | mobile-app | SENIOR | sentry.init in app/_layout, posthog events registry |
| ⭐ | Two-step token refresh deduplication | mobile-app | SENIOR | src/api/client.ts, actor-isolated refresh |
|   | Standard Expo Router setup | mobile-app | SOLID | app/ folder structure |
|   | Hilt dependency injection (basic) | — | BASELINE | (not used in this project) |

## TechStack revision

{Filled by Phase 6.5. One of three cases:

CASE A — kept as-is:
**Decision**: kept as-is. The existing techStack is already strong.
**Current**: "{existing techStack string}"

CASE B — replaced:
**Decision**: replaced.
**Before**: "{old techStack}"
**After**: "{new techStack}"
**Added**: {tech1 (why), tech2 (why)}
**Removed**: {tech (why)}
**Kept**: {tech list}

CASE C — new entry, no prior techStack:
**Decision**: composed from scratch.
**Composed**: "{new techStack string}"
**Rationale**: {brief selection criteria}
}

## Duplicate warnings

{Filled by Phase 6.6 Part B ONLY when cross-project duplicates are detected. Skip the
whole section if none.

- ⚠️  Bullet "Expo SDK 46 → 54 migration with breaking-change fixes" resembles
  "Migration Expo SDK 49 → 53" in another project's entry. Composition was not modified —
  your call whether to keep both, edit one, or remove one.
}

## Repo metrics

{Multi-repo: one subsection per repo. Single-repo: just one block.}

### {repo-name}
- Commits: {N user / M total} ({user_share_pct}% share)
- Active days: {N}
- Conventional commits: feat={N}, fix={N}, refactor={N}, test={N}
- feat:fix ratio: {ratio}
- Test coverage signal: {pct}% of commits touch test files
- Average commit size: {N} lines
- **PRs authored**: {total} total — {merged} merged, {closed} closed, {open} open
  {OR: "PRs: unavailable (gh not configured / not authenticated / repo not on GitHub)"}

## Chosen for CV ({count})

### Polish bullets
1. "..."

### English bullets
1. "..."

## Notes

{Optional: caveats, things noticed but not confidently categorized, suggestions for
future iterations}
```

## Column conventions

- **Status**: ⭐ for items chosen for the final bullets, empty otherwise.
- **Item**: 1-line description of the achievement/decision.
- **Source**: which repo(s) the item came from, comma-separated. **Hide this column
  entirely if only one repo was analyzed.**
- **Category**: FLAGSHIP / SENIOR / SOLID / BASELINE.
- **Evidence**: brief pointer to where it can be verified — file path, commit message,
  git-log fragment. For the user's reference (interview prep), not for the recruiter.
