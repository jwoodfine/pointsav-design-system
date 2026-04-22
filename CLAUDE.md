# CLAUDE.md — pointsav-design-system

PointSav's design system. Canonical repo:
`github.com/pointsav/pointsav-design-system`. This file is
repo-specific and inherits the workspace rules in `~/Foundry/CLAUDE.md`
(auto-loaded by Claude Code). Read that first for corporate topology,
identity map, commit flow, and rules of engagement.

## Tier

**Engineering tier.** Participates in the Jennifer/Peter staging-tier
flow described in `~/Foundry/CLAUDE.md §2`. Not admin-only.

## Remotes

| Name | URL | Role |
|---|---|---|
| `origin` | `git@github.com:pointsav/pointsav-design-system.git` | Canonical (vendor). Do not push directly; Stage 6 `tool-promote.sh` handles staging → canonical promotion |
| `origin-staging-j` | `git@github.com-jwoodfine:jwoodfine/pointsav-design-system.git` | Staging mirror on Jennifer's account |
| `origin-staging-p` | `git@github.com-pwoodfine:pwoodfine/pointsav-design-system.git` | Staging mirror on Peter's account |

Current staging-tier policy for this repo: push every commit to both
staging remotes so they stay in sync as mirrors. Jennifer/Peter
alternating attribution is visible in both commit logs.

## Commit and push procedure

Follow `~/Foundry/CLAUDE.md §7` staging-tier procedure to commit, then:

```
git push origin-staging-j main
git push origin-staging-p main
```

Both should be fast-forward. Do not push to `origin` (canonical)
without explicit operator approval — canonical is the promotion
target, not a staging target.

## Branch convention

Single `main` branch. Linear history. No feature branches for
routine changes.

## Content

Design tokens (YAML), brand signets (SVG/PNG), icon set, CSS
scaffolding, design documents. See `README.md` for the full
file-typology catalogue.
