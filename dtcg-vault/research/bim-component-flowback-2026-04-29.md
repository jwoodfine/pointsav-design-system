---
schema: foundry-design-research-v1
component_or_token: sidebar-accordion, code-block-with-copy, chip-row, tab-bar-disclosure, preview-frame, empty-state-card, machine-surface-footer, edit-on-github-link
decision_type: component-flowback
authored: 2026-05-06
authored_by: project-design Task (sweep of project-bim draft design-generic-components-index.md)
authored_with: claude-sonnet-4-6
status: staged
originating_cluster: project-bim
brand_voice_alignment: [direct, precise, professional]
accessibility_targets: [wcag-2-2-aa]
ai_consumption_hint: "Eight component stubs added to the META-substrate from project-bim v0.0.2 flowback. Read this file for provenance, naming resolution, and deferred items before generating any of these components."
---

# BIM component flowback — 9 patterns from project-bim v0.0.2

Source draft: `project-bim/.agent/drafts-outbound/design-generic-components-index.md`
(2026-04-29, `authored_with: claude-opus-4-7`, research_done_count: 5).

project-bim v0.0.2 identified nine domain-agnostic component patterns built
during its visual upgrade. Per operator policy ("we should be sending back all
the COMPONENTS used to project-design with research for future development"),
these were forwarded to project-design META-substrate via the
cluster-design-draft-pipeline.md sweep.

---

## Naming convention decision (open question resolved)

The draft's open question asked whether META-substrate generic versions should
adopt the `bim-` class-naming convention (e.g., `.bim-chip__label`) or a
parallel `ps-` naming.

**Resolution:** `ps-` prefix throughout — consistent with the existing substrate
vocabulary (`ps-btn`, `ps-tabs`, `ps-crumbs`). This makes tenant surfaces that
consume both BIM-specific and generic components coherent. BIM cluster code
(`.bim-*`) stays cluster-internal on `cluster/project-bim`; the generic forms
here use `ps-*`.

---

## 8 stubs committed (out of 9)

| Draft name | Component name | Status | Notes |
|---|---|---|---|
| SidebarAccordion | `sidebar-accordion` | stub | Categorised left-rail navigation with active state |
| CodeBlockWithCopy | `code-block-with-copy` | stub | Pre + copy-to-clipboard button with 1.4 s revert |
| ChipRow | `chip-row` | stub | Six semantic variants (default/primary/accent/neutral/warning/success) |
| TabBarDisclosure | `tab-bar-disclosure` | stub | `<details>`-based tabs; differs from URL-reflected `ps-tab` |
| PreviewFrame | `preview-frame` | stub | Light/dark theme toggle; data-theme attribute pattern |
| EmptyStateCard | `empty-state-card` | stub | Dashed-border no-data surface |
| MachineSurfaceFooter | `machine-surface-footer` | stub | Three-column machine surface footer |
| EditOnGitHubLink | `edit-on-github-link` | leg-pending | Not yet implemented in BIM v0.0.2; operator direction needed |

## Not added — BreadcrumbNav

The draft included `BreadcrumbNav` (`.bim-crumbs`). The META-substrate already
ships `breadcrumb` (`ps-crumbs`) with equivalent functionality: `<nav
aria-label>` wrapping an `<ol>`, `::after` separator content (not inline
glyphs), `aria-current="page"` on the current item. No new component needed;
BIM cluster can consume `ps-crumbs` directly.

## Not added — BIM-specific components

The draft explicitly excluded: `BimSpatialTree`, `BimPropertiesPanel`,
`BimViewport3D`, `BimClassificationChip`, `BimCodeOverlayPanel`,
`IsometricBuildingMassHero`, `BimGuidLabel`. These remain in
`pointsav-design-system/components/bim-*/` on `cluster/project-bim` — they
are AEC-domain-specific and do not belong in the generic META-substrate.

---

## Next steps for each stub

Each `recipe.json` stub carries the structural shape, token references, and
ARIA notes. Subsequent milestones add:
- Full CSS inline in `recipe.json`
- `accessibility.md` — WCAG 2.2 criterion-by-criterion table
- `code.md` — rendered code examples
- `style.md` — visual specification
- `usage.md` — when/when-not guidance

`edit-on-github-link` is additionally blocked on operator direction for the
GitHub URL template.
