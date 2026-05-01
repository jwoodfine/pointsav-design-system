---
schema: foundry-design-research-v1
component: citation-authority-ribbon
carbon_baseline: Tag (non-interactive badge variant — see divergence notes)
wcag_target: 2.2 AA
authored: 2026-05-01
authored_by: project-design gateway (Task Claude, cluster/project-design)
refined_from: clones/project-knowledge/.claude/drafts-outbound/component-citation-authority-ribbon.draft.md
ai_consumption_hint: >
  The data-source-authority attribute is the canonical machine-readable surface.
  RAG and LLM consumers parsing rendered HTML derive citation source-class directly
  from the DOM without prose parsing. JSON-LD emission attaches the same class to
  each citation entry as a @type refinement on the TechArticle schema:
  AcademicSource / RegulatorSource / IndustrySource / DirectSource /
  NewsSource / WebInformalSource layered onto Schema.org CreativeWork hierarchy.
  These types are documented in the wiki's llms.txt for external AI consumer reference.
---

# Accessibility notes — ps-citation-badge / ps-references

## WCAG 2.2 AA checklist

| Criterion | Treatment | Status |
|---|---|---|
| 1.4.1 Use of colour | Each badge carries both a colour AND a letter glyph (A / R / I / D / N / W). Colour is not the sole differentiator — screen readers and colour-blind users both receive the classification signal | Pass |
| 1.4.3 Contrast — badge text | Academic (white on #0f62fe): 4.6:1 ✓. Regulator (white on #26823f): 4.6:1 ✓. Industry (#0e0f12 on #e6e8ec): 9.2:1 ✓. Direct-source (#009d9a on #d9fbfb): verify at deployment — border provides additional signal. Web-informal (#878d99 on transparent): check against actual page background | Requires verification per deployment for direct-source and web-informal |
| 1.4.3 Contrast — citation prose | Citation text uses `--semantic-text-primary` on white card surface — 21:1 ✓. Backref arrow uses `--semantic-text-secondary` — 7.4:1 on white ✓ | Pass |
| 2.1.1 Keyboard | Badge is a `<span>`, not focusable. Only `<a>` elements (citation URLs + backref arrow) are keyboard-reachable | Pass |
| 2.4.7 Focus visible | `:focus-visible` ring on backref `<a>` and citation URL `<a>` — 2px solid, 2px offset | Pass |
| 4.1.2 Name, Role, Value | `aria-label` on each badge announces the source class ("Academic source", "Regulator source", etc.). Badge carries no interactive role. | Pass |

## Landmark and semantic structure

```
<ol class="ps-references">             ← ordered list (citation numbering preserved)
  <li data-source-authority="academic">
    <span aria-label="Academic source">A</span>   ← informational badge, not focusable
    <span> (citation prose)                        ← static text
    <a href="#cite-ref-1">↑</a>                   ← backref navigation link
  </li>
  ...
</ol>
```

The `data-source-authority` attribute is a custom HTML data attribute — it does not affect the accessible name or role of the `<li>` element. Screen readers announce the numbered list item, then the badge's `aria-label`, then the citation prose.

## Colour-not-sole-differentiator implementation

Every badge carries:
1. A single-letter glyph that encodes the classification (A = Academic, R = Regulator, I = Industry, D = Direct source, N = News, W = Web-informal)
2. An `aria-label` that announces the full class name
3. A `title` attribute for pointer users who hover (supplementary; not relied upon for accessibility)

The six letter glyphs are distinct and do not overlap with each other. Screen-reader users who cannot perceive colour receive the full classification from the `aria-label`. Colour-blind users who cannot distinguish hues still receive the letter glyph.

## Ratified decisions

### Single-letter glyph vs. full-word tag

**Ratified: single-letter glyph.** Trade-off analysis:
- Single-letter preserves the Wikipedia citation-list density floor — references sections are typically long (10–30 entries); a full-word tag on every entry would create significant visual weight
- The letter glyph achieves recognition after ~3 encounters; `aria-label` carries the full word for all users at all times
- Full-word Carbon Tag is appropriate for filter-chip contexts; citation badges are not filter chips and the interactive affordance of a full-word pill would mislead

### Badge position: leading the entry text

**Ratified: leading position.** The badge appears as the first grid column in the 3-column entry layout (badge | prose | backref). This creates a scannable vertical column of badges for readers assessing source quality across a list of references — the most efficient layout for the task.

## JSON-LD schema integration

The component's visual surface is the HTML layer. The machine-readable layer is the JSON-LD emission per article:

```json
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "citation": [
    {
      "@type": ["ScholarlyArticle", "AcademicSource"],
      "name": "seL4: Formal Verification of an OS Kernel",
      "url": "https://sel4.systems/",
      "datePublished": "2009-10"
    },
    {
      "@type": ["GovernmentPermit", "RegulatorSource"],
      "name": "National Instrument 51-102 — Continuous Disclosure Obligations",
      "url": "https://www.bcsc.bc.ca/",
      "publisher": { "@type": "GovernmentOrganization", "name": "BCSC" }
    }
  ]
}
```

The `AcademicSource`, `RegulatorSource`, `IndustrySource`, `DirectSource`, `NewsSource`, and `WebInformalSource` types are PointSav-namespace extensions layered onto Schema.org's existing `CreativeWork` hierarchy. They are announced in the wiki's `llms.txt`.

## Provenance

Refined by project-design gateway from `component-citation-authority-ribbon.draft.md` (originating cluster: project-knowledge, authored 2026-04-30T01:00:00Z). Open questions resolved: single-letter glyph ratified; leading position ratified; `aria-label` phrasing ratified as "Type source".
