# dtcg-vault — vault template

[ 🇪🇸 Leer este documento en Español ](./README.es.md)

This directory is the **canonical template** for a per-tenant
vault under Doctrine claim #38 (Design System Substrate). It is the
content `app-privategit-design` reads from disk at runtime —
distinguished here from the existing top-level `tokens/`,
`components/`, `themes/`, `templates/`, `guidelines/`, `docs/` trees
which carry the prior YAML-canonical layer consumed by sibling
clusters (`project-orgcharts`).

## How it is used

| Context | Path |
|---|---|
| Vendor showcase | `~/Foundry/deployments/vault-privategit-design-1/` (this content seeds it) |
| SMB customer fork | `<their-clone-of-app-privategit-design>/dtcg-vault/` → bootstrap copies into their `vault-privategit-design-1/` |

## Layout

```
dtcg-vault/
├── tokens/        — DTCG primitive + semantic + component layers
├── themes/        — per-brand semantic-layer overrides (pointsav-brand.json today)
├── components/    — HTML+CSS+ARIA recipe files (button-primary.json today)
├── research/      — AI-readable design-decision rationale
└── exports/       — derived caches (Figma, Tailwind, Style Dictionary; populated at build time)
```

`tokens/`, `themes/`, `components/`, `research/`, `exports/` are
the five canonical layers per the substrate engine's expectations.

## v0.0.1 contents

- `tokens/primitive.json` — Carbon-baselined DTCG primitive layer
  (color, type, space, motion, focus)
- `themes/pointsav-brand.json` — PointSav semantic-layer override +
  voice rules + accessibility commitments
- `components/button-primary.json` — first component recipe
- `research/design-philosophy.md` — substrate doctrine narrative
- `research/carbon-baseline-rationale.md` — primitive layer rationale

Subsequent milestones add component recipes (`input-text`,
`link-primary`, `surface-elevated`, `notification-toast`,
`navigation-bar`), semantic layer expansion, and
`exports/figma-variables.json` / `exports/style-dictionary.json`
derived builds.

## Why this directory exists separately from `tokens/`, `themes/`, `components/` at repo root

The repo root carries the prior YAML-canonical layer
(`tokens/global/`, `tokens/semantic/`, `themes/MEMO-Woodfine-Color-Matrix.md`,
`components/*.css`, `templates/`, `guidelines/`) consumed by
project-orgcharts as its DOWNSTREAM input. The substrate cluster
(`project-design`) introduces DTCG as the new canonical form per
claim #38; the two coexist during the migration window.

`dtcg-vault/` is the substrate-canonical form. Migration of the
prior YAML layer into DTCG happens in subsequent milestones,
coordinated with project-orgcharts to avoid breaking their consumer
contract. See cluster manifest `cross_cluster_dependencies` for the
coordination interface.
