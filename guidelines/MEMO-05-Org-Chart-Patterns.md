# MEMO-05: Org-Chart & Structural-Diagram Patterns
### *Hierarchical Visualizations from Design-System Primitives*

**Status: Active** | **Applies to: Corporate org charts, SPV/fund structural diagrams, relationship diagrams**
**First content driver:** Woodfine Investor Relations SPV Arrangements chart (project-orgcharts cluster, 2026-04-25)

---

## 1. Scope

Hierarchical and structural visualizations — org charts, SPV arrangement diagrams, fund structures, board-and-committee maps — built from the same set of CSS primitives. Source material is typically a PowerPoint export with absolute-positioned shapes; the design-system equivalents replace that with semantic HTML and CSS Grid.

The components in this memo emerged from authoring the Woodfine SPV Arrangements chart and are reusable for any chart that arranges entity nodes in panels with role labels and connector lines.

## 2. Component Surface

Three component files compose a chart:

* **`components/chart.css`** — Chart canvas (`.spv-chart`), header with title and legend (`.spv-chart__header`, `.spv-chart__legend`), row layout (`.spv-chart__row--top`, `.spv-chart__row--bottom`), per-panel container (`.spv-panel`, `.spv-panel__title`, `.spv-panel__diagram`), dashed wrapper for funds (`.fund-wrapper`), footnote (`.spv-chart__footnote`).
* **`components/nodes.css`** — Entity rectangles (`.entity-node`), role labels (`.role-badge`, `--lead`, `--ellipsis` modifiers), footnote marker (`.footnote-marker`).
* **`components/connectors.css`** — Vertical drop line (`.connector-vertical`, `--short`), horizontal bus for one-to-many fan-out (`.lp-bus`), fan-out cell containers (`.lp-row`, `.lp-cell`).

Names use the `spv-` prefix where the structure encodes investment-vehicle semantics (panels, fund wrapper); generic primitives (`entity-node`, `role-badge`, `connector-*`, `lp-*`) carry their own short names for reuse across chart types.

## 3. Composition Pattern

A panel always nests in this order:

```
spv-panel
  spv-panel__title
  spv-panel__diagram
    role-badge                  (optional label above the top entity)
    entity-node                 (the GP / top of hierarchy)
    connector-vertical          (drop)
    [ entity-node + role-badge ]   (single LP, sole investor)
    OR
    [ lp-bus + lp-row of lp-cell entries ]   (fan-out, club deal / fund)
```

For the Fund variant, the LP fan-out sits inside `.fund-wrapper`, which carries the `.fund-wrapper__label` ("Fd") in its top-left corner.

## 4. Theming

Chart components consume the existing Tier-2 system tokens (`--sys-canvas`, `--sys-card`, `--sys-text`, `--sys-border`, `--sys-hairline`, `--sys-accent`) defined in `tokens/theme-generic.css` and overridden in `tokens/theme-woodfine.css`. No chart-specific tokens are introduced — by design. A theme switch (e.g., PointSav vs Woodfine) re-themes the chart without touching component CSS.

The dashed Fund container uses `--sys-text` for its border so it reads as structural rather than accented; the Fund label uses `--sys-accent` (Woodfine Blue Base `#164679`) as the only chromatic anchor in the chart.

## 5. Print Egress

Each component file carries a small `@media print` block that flattens hairline borders to pure black `#000`, removes card-background fills, and inverts the Fund label to black-on-white. Combined with a page-level `@page { size: 13.3333in 7.5in }` declaration in the chart artifact, the chart prints to landscape Letter or to the legacy slide size used in the source PowerPoint.

The print rules deliberately do not live in `egress.css` — that file owns marketing-page print mechanics. Chart print egress co-locates with each component so the chart artifact stays self-contained.

## 6. Compositional Rules

* **One legend per chart, top-right.** GP / LP definitions sit as small bordered cards in the chart header; do not repeat them per panel.
* **Same connector weight throughout.** All `.connector-vertical` and `.lp-bus` use `2px` solid `--sys-text`. Don't introduce per-panel weight variation.
* **Ghost vs bordered entities.** All `.entity-node` rectangles carry a visible border. The PowerPoint source occasionally rendered GPs without borders; that is treated as a tooling artifact and normalized to bordered-everywhere in the design-system rendering.
* **Ellipsis means "and so on."** A `.role-badge--ellipsis` paired with an `.entity-node` containing `…` represents an unbounded list of additional entries. Do not render specific counts beyond what the source data warrants.
* **No competitive comparison in chart copy.** Per `~/Foundry/CLAUDE.md` §6 structural-positioning rule, panel titles describe the structure (`Investment Banking`, `Asset Management`) without contrasting against external platforms.

## 7. BCSC Disclosure Posture

Per `~/Foundry/CLAUDE.md` §6 rule 2, charts that depict relationships between named legal entities (subsidiary/parent, GP/LP arrangements with named investors) only render those entities when documented and current in the corporate record. Generic placeholder labels (`Investor A`, `Lead Investor`, `Manager`) used for template charts are not subject to this rule; named-investor charts are.

## 8. Out of Scope

This memo covers static structural diagrams. Interactive features (hover tooltips, drill-down, click-to-expand) are not part of v1; if and when they ship, they belong in a separate `chart-interactive.css` and a separate ADR.

---
*© 2026 PointSav Digital Systems™ | Architecture & Design Protocols*
