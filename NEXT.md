# NEXT.md — pointsav-design-system

> **Scope: this repo only.** Cross-repo and workspace-level open
> items live at `~/Foundry/NEXT.md`.
>
> Read at session start when a Root Claude opens in this repo. Update
> at session end when repo-scope open items change.

Last updated: 2026-04-28.

---

## Currently open

- **Confirm bilingual README compliance at repo root.** Per the
  2026-04-22 audit, `README.md` is present; verify `README.es.md` is
  current and correctly paired. Repo carries design-system assets
  and tokens that downstream repos depend on — bilingual documentation
  matters.
- **Consider per-sub-asset documentation.** The `tokens/`, `assets/`,
  `components/`, `themes/`, and `templates/` subdirectories are the
  design-system's working areas. They do not yet carry their own
  `CLAUDE.md` / `NEXT.md`. Decide whether they need them — this repo
  is a single coherent artefact per the framework, so the answer may
  be "no," but worth settling explicitly.

## Recently added (2026-04-28)

- Woodfine Color Matrix MEMO extended (`themes/MEMO-Woodfine-Color-Matrix.md`).
  Adds the full Woodfine brand palette (`--wf-blue`, `--wf-green`,
  `--wf-orange`, `--wf-red`, `--wf-purple`, `--wf-gold`) plus
  the neutral scale (`--ink` through `--ink-4`, `--rule`,
  `--rule-strong`) and the per-chart accent rule (single `--accent`
  bound per chart per domain — blue for counsel/governance, green
  for accounting/finance/ops). Backfilled from the Apr 15 JW14
  Accounting / Counsel pair + Apr 6 JW9 Accounting Statements
  consolidation chart authored in the project-orgcharts cluster.
- Org-chart printable template (`templates/html/org-chart-printable.html`).
  Single-template, accent-swappable chart skeleton — title block +
  4 sections (board / management / offices / disciplines) +
  signature, on a 1056×816 US Letter landscape canvas. Drives all
  future Woodfine corporate org-chart authoring; replaces the
  ad-hoc PowerPoint export pattern that the legacy charts used.

## Recently added (2026-04-27)

- Chart component family — `components/chart.css`,
  `components/nodes.css`, `components/connectors.css`, plus
  `guidelines/MEMO-05-Org-Chart-Patterns.md`. Backfilled from the
  Woodfine SPV Arrangements chart authored in the project-orgcharts
  cluster. Surface: chart canvas + panel + entity-node + role-badge
  + connector primitives, themed via existing `--sys-*` tokens. See
  the memo for composition rules and theming guidance.

## Recently closed (2026-04-22)

- Audit cleanup — 7 tracked `.DS_Store` files removed across
  `assets/`, `tokens/`, and their subdirectories. `.gitignore`
  created with `.DS_Store` entry. Commit `015d074`.

## Pointers

- Workspace-level open items: `~/Foundry/NEXT.md`
- Workspace changelog: `~/Foundry/CHANGELOG.md`
- Repo-level `CLAUDE.md`: `CLAUDE.md` (repo-level rules; first
  per-repo `CLAUDE.md` in the Foundry flow, added 2026-04-21).
