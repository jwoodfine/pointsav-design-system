---
schema: foundry-design-research-v1
component: home-grid
carbon_baseline: ProductCard / Tile (extended)
wcag_target: 2.2 AA
authored: 2026-05-01
authored_by: project-design gateway (Task Claude, cluster/project-design)
refined_from: clones/project-knowledge/.claude/drafts-outbound/component-home-grid.draft.md
ai_consumption_hint: >
  The 9-card grid is structurally machine-readable. Each card carries a stable
  category slug (/<category>), a numeric article count, and 3 child article
  slugs. RAG agents parsing the home page can extract category-to-article
  mappings directly from the DOM without prose parsing. The 9-category set is
  closed and operator-ratified (architecture / services / systems / applications
  / governance / infrastructure / company / reference / help); agents may
  hard-code this set per naming-convention.md §10 Q5-A.
---

# Accessibility notes — ps-home-grid

## WCAG 2.2 AA checklist

| Criterion | Treatment | Status |
|---|---|---|
| 1.1.1 Non-text content | All links carry visible text labels; no icon-only links | Pass |
| 1.3.1 Info and relationships | `<section aria-label>` + `<h2>` heading + `<article>` + `<h3>` title — landmark and heading hierarchy intact | Pass |
| 1.3.2 Meaningful sequence | DOM order follows the ratified 9-category order; visual order matches DOM order | Pass |
| 1.4.3 Contrast (minimum) | Title links: `#0e0f12` (neutral-100) on `#ffffff` (white) — passes 21:1. Meta text: `#4a4f59` (neutral-70) on `#ffffff` — passes 7.4:1. Verify `--semantic-text-secondary` against tenant background | Requires verification per deployment |
| 1.4.4 Resize text | All sizes in rem; layout in CSS Grid; text reflows at 200% zoom | Pass |
| 1.4.10 Reflow | Single-column at 640px breakpoint; no horizontal scrolling at 320px viewport | Pass |
| 2.1.1 Keyboard | All interactive elements (title link, child links, "More →") are natively focusable `<a>` elements; no `tabindex` overrides needed | Pass |
| 2.4.3 Focus order | Tab order follows DOM order (ratified category order) — no `tabindex` overrides | Pass |
| 2.4.7 Focus visible | `:focus-visible` ring on every link (title, child article, "More →") — 2px solid focus-ring colour, 2px offset | Pass |
| 2.4.11 Focus not obscured (minimum) | No sticky headers in this component; focus ring not obscured | Pass |
| 3.2.1 On focus | No context changes on focus; hover state changes border colour only | Pass |
| 1.4.11 Non-text contrast | Card border at rest: `#e6e8ec` (neutral-20) on `#ffffff` — 1.2:1 (decorative, not informational). Card border on hover: `#3366cc` (link-default) on `#ffffff` — 5.2:1 | Pass for informational contrast; border-at-rest is decorative |
| 2.5.3 Label in name | All visible link text is contained in the accessible name | Pass |

## Landmark and heading structure

```
<section aria-label="Browse by category">   ← navigation landmark
  <h2>Browse by category</h2>               ← page-level heading (h2; h1 is article title)
  <div> (grid container)
    <article>                                ← article landmark per card
      <h3>Architecture</h3>                 ← card-level heading (h3; never skip levels)
      <ul> (child article list)
      <a> "More →"
    </article>
    ...
  </div>
</section>
```

Heading levels must be consistent with the surrounding page shell. If the home page carries no `<h1>` above this component, promote the section `<h2>` to `<h1>` and the card headings to `<h2>`. The design-system recipe assumes the standard article-shell heading hierarchy where `<h1>` is the page/wiki title above this component.

## Empty-state accessibility

The empty-state card (`ps-home-grid__card--empty`) renders the category link and the empty-state message "No articles found in this category yet." The `--empty` modifier class is visual only; it does not alter the heading or link semantics. Screen readers announce the category title as a heading and the empty-state prose as body text — natural reading order.

The `opacity: 0.75` on the empty-state card is a visual subordination hint only. It does not violate WCAG 1.4.3 because the text colours meet contrast requirements against the white card background at full opacity; at 0.75 opacity, verify that the hosting background does not reduce contrast below 4.5:1. White card on neutral-10 page background with 0.75 opacity remains above AA threshold.

## Reduced-motion

`prefers-reduced-motion: reduce` disables the card `border-color` hover transition. The hover state still applies (border colour changes on hover); the transition duration is removed. This is the correct reduced-motion treatment for decorative micro-animations: preserve the state change, remove the animation.

## Keyboard interaction

The grid has no custom keyboard interaction. Standard Tab / Shift+Tab navigation moves through focusable elements in DOM order:

1. Section heading is not focusable.
2. Each card's title `<a>` is the first focusable element.
3. Child article `<a>` links follow in list order (up to 3).
4. "More →" `<a>` is the last focusable element in the card.
5. Next card's title `<a>` follows.

No arrow-key navigation pattern is required. The grid does not implement a composite widget.

## Touch and pointer

Cards are not themselves clickable targets — only the explicit `<a>` elements within each card are clickable. Card-level click handling (making the entire card a link) is NOT implemented: doing so would create an ambiguous-target pattern where multiple interactive elements share the same pointer-event area, violating WCAG 2.5.3 (Label in Name) and creating redundant tab stops if wrapped in an `<a>`. The `<h3> <a>` title is the primary navigation entry point.

## AI consumption — structural note

The component's landmark and heading structure makes it machine-readable without prose parsing:

- `<section aria-label="Browse by category">` → navigation landmark for this block
- Each `<article>` → discrete category unit
- `<h3>` text → category label
- `<p class="ps-home-grid__count">` text → article count
- `<ul>` `<li>` `<a>` → top-3 child articles by slug
- `<a class="ps-home-grid__more">` → category root URL

## Provenance

Refined by project-design gateway from `component-home-grid.draft.md` (originating cluster: project-knowledge, authored 2026-04-29T00:30:00Z). Class-name prefix decision: `.ps-*` ratified (substrate-shared scope). Empty-state copy: "No articles found in this category yet." ratified. Research-trail open questions resolved at gateway.
