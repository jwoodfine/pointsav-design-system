---
schema: foundry-design-research-v1
component: research-trail-footer
carbon_baseline: Accordion (single-item disclosure variant)
wcag_target: 2.2 AA
authored: 2026-05-01
authored_by: project-design gateway (Task Claude, cluster/project-design)
refined_from: clones/project-knowledge/.claude/drafts-outbound/component-research-trail-footer.draft.md
ai_consumption_hint: >
  The substrate emits the research trail as JSON-LD potentialAction nodes on
  the article's TechArticle schema. SearchAction nodes encode suggested research
  items; Question nodes encode open questions. LLM consumers can identify the
  article's epistemic frontier — what is known, what should be researched next,
  what remains unanswered — without parsing article prose. Category field
  distinguishes research-suggested from research-open.
---

# Accessibility notes — ps-research-trail

## WCAG 2.2 AA checklist

| Criterion | Treatment | Status |
|---|---|---|
| 1.3.1 Info and relationships | Native `<details>/<summary>` — browser assigns `role="group"` to details; summary is the button that toggles it. `<section aria-label>` wraps the body | Pass |
| 1.4.1 Use of colour | Subsection headings use coloured left-border; heading text provides the full classification ("Research done", "Suggested research", "Open questions"). Colour not sole differentiator | Pass |
| 1.4.3 Contrast — summary | `--semantic-text-secondary` on `--semantic-surface-layer-accent` → #4a4f59 on #e6e8ec → 3.9:1. Below 4.5:1 — mitigation: summary is `font-weight: 600`, which satisfies large-text rule (3:1 at ≥ 18pt or 14pt bold). Verify at 0.875rem × 600-weight = 12.25px bold. The WCAG large-text threshold is 14pt (18.67px) — this falls below large-text at typical DPI. Flag for production verification. | Requires production verification |
| 1.4.3 Contrast — body text | `--semantic-text-primary` on `--semantic-surface-layer-accent` → #0e0f12 on #e6e8ec → 13.5:1 ✓ | Pass |
| 2.1.1 Keyboard | Native `<details>/<summary>` is keyboard-togglable (Space / Enter) in all modern browsers without JS | Pass |
| 2.4.7 Focus visible | `:focus-visible` ring on summary — 2px solid focus-ring colour, 2px offset | Pass |
| 4.1.2 Name, Role, Value | `<details>` has no explicit ARIA; browsers map natively. `<summary>` is announced as button. `aria-expanded` is managed by the browser natively for `<details>` | Pass |

## Landmark and heading structure

```
<details class="ps-research-trail">               ← native disclosure widget
  <summary>Research trail — N done · N suggested · N open</summary>
  <section aria-label="Research trail detail">    ← content region
    <h3 id="research-trail-done">Research done</h3>      ← subsection heading
    <ul> (Done items)
    <h3 id="research-trail-suggested">Suggested research</h3>
    <ul> (Suggested items)
    <h3 id="research-trail-open">Open questions</h3>
    <ul> (Open question items)
  </section>
</details>
```

The `<h3>` level is correct when the article body contains "## Research trail" rendered as `<h2>`, and the engine inserts this `<details>` block under that `<h2>`. If the heading level in the surrounding context is different, the `<h3>` elements should be adjusted to maintain no-skip hierarchy.

## Ratified decisions

### Collapsed by default (chrome posture)

**Ratified.** The research trail is subordinate to the article body. Readers arrive for the article content; the trail is for researchers, regulators, and editorial-curious readers. Collapsed-default respects the article reading experience. The summary line exposes the counts ("4 done · 3 suggested · 1 open question") at all times — readers get the density signal without expanding.

### trail-bg: chrome posture (semantic.surface.layer-accent)

**Ratified.** The muted neutral surface (`#e6e8ec`) signals that the research trail block is structural chrome, not body content. This resolves §7(f) of the research draft: chrome posture. The left-border accent reinforces the chrome / structural-element register.

### Native `<details>/<summary>` over Carbon Accordion

**Ratified.** The research trail is a single disclosure item. Carbon Accordion's multi-item pattern, expand-all/collapse-all controls, and JS dependency add complexity without benefit. Native `<details>` delivers keyboard navigation, screen-reader announcement, and `aria-expanded` state management natively — zero JS, full browser compatibility (all modern browsers since 2016).

## JSON-LD machine-readable surface

```json
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "potentialAction": [
    {
      "@type": "SearchAction",
      "name": "seL4 capability-revocation 2024–2026 papers — verify transitive revocation behaviour",
      "category": "research-suggested"
    },
    {
      "@type": "SearchAction",
      "name": "Cross-reference with NetBSD compatibility layer's capability mapping",
      "category": "research-suggested"
    },
    {
      "@type": "Question",
      "name": "Does the seL4 microkernel revoke capabilities transitively when a parent capability is destroyed?",
      "category": "research-open"
    }
  ]
}
```

## Engine integration notes (project-knowledge cluster scope)

The substrate ships the recipe; the engine (app-mediakit-knowledge) implements the render-time machinery:

1. **Count extraction**: read `research_done_count`, `research_suggested_count`, `open_questions_count` from article frontmatter — inject into summary line text at render time
2. **Section detection**: identify the "## Research trail" markdown heading; render the `<details>` block in its place
3. **Subsection parsing**: parse the three canonical subsections (Done / Suggested / Open questions) from the article body under the "## Research trail" heading into the three `<ul>` elements
4. **JSON-LD emission**: emit `SearchAction` and `Question` nodes for suggested / open items respectively

These are project-knowledge cluster scope for the next engine iteration.

## Provenance

Refined by project-design gateway from `component-research-trail-footer.draft.md` (originating cluster: project-knowledge, authored 2026-04-30T01:05:00Z). Open questions resolved: collapsed-default ratified (chrome posture); trail-bg → semantic.surface.layer-accent (chrome posture); render-time count injection deferred to engine (project-knowledge scope).
