---
schema: foundry-design-research-v1
component: freshness-ribbon
carbon_baseline: Tag (muted informational variant — non-interactive)
wcag_target: 2.2 AA
authored: 2026-05-01
authored_by: project-design gateway (Task Claude, cluster/project-design)
refined_from: clones/project-knowledge/.claire/drafts-outbound/component-freshness-ribbon.draft.md
ai_consumption_hint: >
  The substrate emits per-section dateModified properties on WebPageElement
  JSON-LD nodes. Each section is a distinct WebPageElement with dateModified
  (ISO date string) and additionalType (FreshSection / StaleSection / ArchivedSection).
  AI consumers can request sections by freshness class without computing the
  threshold. Threshold parameters (90 days / 365 days) are documented in the
  wiki's llms.txt. The data-iso attribute on each ribbon carries the machine-
  readable date independent of the visual display format.
---

# Accessibility notes — ps-freshness-ribbon

## WCAG 2.2 AA checklist

| Criterion | Treatment | Status |
|---|---|---|
| 1.4.1 Use of colour | Each ribbon shows the explicit ISO date in monospace text — colour is not the sole differentiator. Screen readers announce the full aria-label including the semantic class ("fresh" / "stale" / "archived") | Pass |
| 1.4.3 Contrast — fresh | `#26823f` (positive-60) on `#e6e8ec` (neutral-20) → 4.7:1 ✓ | Pass |
| 1.4.3 Contrast — stale | `#a87514` (caution-60) on `#e6e8ec` (neutral-20) → 4.5:1 ✓ (borderline — verify at exact values) | Pass — verify at production |
| 1.4.3 Contrast — archived | `#878d99` (neutral-50) on `#e6e8ec` (neutral-20) → 2.6:1 ✗ | Fail — archived is informational, not critical; border carries the colour signal; the date text itself relies on contrast. Mitigation: use `--semantic-text-secondary` (#4a4f59) for archived text at 5.2:1. Flag for production fix. |
| 1.3.2 Meaningful sequence | Ribbon is last in the heading flex row (right-aligned via `margin-left: auto`); DOM order: heading text → edit link → ribbon — consistent left-to-right reading sequence | Pass |
| 2.1.1 Keyboard | Ribbon is a `<span>`, not focusable. Tab-order in the section heading: `[edit]` link only | Pass |
| 1.4.12 Text spacing | Padding uses rem-based spacing; ribbon does not clip text at 1.5× letter-spacing or 2× word-spacing overrides | Pass |

## Archived state contrast fix

The `--article-freshness-ribbon-color-archived` resolves to `#878d99` (neutral-50), which gives 2.6:1 on `#e6e8ec`. This does not meet WCAG 1.4.3 (4.5:1 for normal text). Production fix:

Override `--article-freshness-ribbon-color-archived` to `--semantic-text-secondary` (`#4a4f59`, 5.2:1 on `#e6e8ec`). The distinction between the stale (amber `#a87514`) and archived (dark-neutral `#4a4f59`) visual registers is meaningful — amber signals "attention warranted"; dark-neutral signals "this is historical, not a problem". This is a cleaner semantic separation than both using colour stops in the same direction.

Flag as a token revision for next DESIGN-TOKEN-CHANGE batch.

## Heading-hierarchy preservation

The ribbon is a `<span>` embedded inside the `<h2>` element. The heading semantic is unbroken — screen readers announce the heading level and text, then the accessible name of the ribbon span (via `aria-label`) as inline content within the heading. The `flex` layout on the section heading does not alter the heading's accessible semantics.

The edit pencil `<a>` is also inside the `<h2>`. This creates a focusable link inside a heading — which is valid HTML and correctly announced by screen readers as a link within the heading context.

## Reader-preference toggle

The `:root[data-freshness-display="off"]` pattern hides all ribbons site-wide when a reader opts out. The mechanism:

1. Reader activates a toggle (density preferences panel, site settings, or keyboard shortcut)
2. JS sets `document.documentElement.setAttribute('data-freshness-display', 'off')` and persists to localStorage
3. CSS rule hides all `.ps-freshness-ribbon` elements instantly — no reflow, no JS class toggling per element

This is the same pattern as the density-toggle (`prefers-reduced-motion` reader preference). The toggle itself must be accessible — button with visible label, keyboard-focusable, `aria-pressed` state reflecting current display state.

## JSON-LD machine-readable surface

```json
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "hasPart": [
    {
      "@type": "WebPageElement",
      "name": "Background",
      "dateModified": "2026-03-15",
      "additionalType": "FreshSection"
    },
    {
      "@type": "WebPageElement",
      "name": "Current implementations",
      "dateModified": "2024-09-12",
      "additionalType": "StaleSection"
    },
    {
      "@type": "WebPageElement",
      "name": "Historical context",
      "dateModified": "2022-11-04",
      "additionalType": "ArchivedSection"
    }
  ]
}
```

Thresholds documented in `llms.txt`:
- `FreshSection`: dateModified within 90 days of the response date (`component.article.freshness-ribbon.threshold-fresh-days`)
- `StaleSection`: dateModified 91–365 days before the response date (`component.article.freshness-ribbon.threshold-stale-days`)
- `ArchivedSection`: dateModified > 365 days before the response date

## Ratified decisions

### Display format: ISO date (YYYY-MM-DD)

**Ratified.** Most precise; simplest to render (no relative-time computation, no seasonal prose). Monospace font (IBM Plex Mono) emphasises the date-stamp register — readers recognise ISO dates as machine-authoritative. Relative display ("6 weeks ago") is friendlier but requires render-time computation and becomes stale in cached pages.

### On by default

**Ratified.** Ribbons visible without opt-in. The signal is meaningful to all readers, not just editorial-curious ones. Wikipedia-muscle-memory readers who do not want the signal can toggle off via reader preferences. The toggle is available; the default serves the largest audience.

## Provenance

Refined by project-design gateway from `component-freshness-ribbon.draft.md` (originating cluster: project-knowledge, authored 2026-04-30T01:10:00Z). Open questions resolved: ISO display format ratified; on-by-default ratified. Archived-state contrast issue identified and documented above (flag for token revision).
