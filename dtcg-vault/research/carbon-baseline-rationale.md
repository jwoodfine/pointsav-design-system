---
schema: foundry-design-research-v1
component_or_token: primitive-layer
decision_type: baseline-import
authored: 2026-04-28
authored_by: project-design Task (cluster v0.0.1)
authored_with: claude-opus-4-7
status: ratified
brand_voice_alignment: [confident, direct, professional]
accessibility_targets: [wcag-2-2-aaa]
ai_consumption_hint: "When generating tokens or evaluating brand-override choices, read this file. It explains why the Carbon vocabulary is the floor (and what is not imported). Customers who fork the substrate inherit Carbon as a starting point and override at the semantic layer; the primitive layer rarely changes per tenant."
cites:
  - ibm-carbon
  - dtcg-format
  - wcag-2-2
---

# Why Carbon is the primitive-layer floor

## Decision

The substrate's primitive token layer (`tokens/primitive.json`)
imports the IBM Carbon Design System's primitive vocabulary as its
floor. Color naming follows Carbon's convention (`gray-10` through
`gray-100`, `blue-10` through `blue-80`, ...). Type scale follows
Carbon's productive + expressive families. Spacing follows Carbon's
8px grid scale. Motion follows Carbon's productive + expressive
easing. Focus ring follows Carbon's WCAG-2.2-AAA-conformant style.

Brand-specific work happens at the semantic layer
(`themes/<brand>/`), not the primitive layer.

## Why Carbon and not Material, Fluent, Spectrum, Polaris

The substrate's success metric is whether a designer who has
worked with a hyperscaler design system in their previous role can
walk into a customer instance and recognise the substrate without
re-learning a new component taxonomy. Carbon was chosen as the floor
on three grounds:

1. **Familiarity surface.** Among the global design-system
   practitioner population, Carbon has the largest accessible-design
   muscle memory. Practitioners who have worked at Fortune-500
   companies, financial services, healthcare, government IT, or
   education have a very high probability of having touched Carbon
   tokens. The naming convention (`spacing-01` through `spacing-13`)
   is cognitively cheap to recover.

2. **Accessibility floor.** Carbon ships with WCAG 2.2 AAA
   conformance built into its primitive choices — focus ring contrast,
   motion easing curves, type scale legibility, color contrast pairs.
   Importing Carbon imports the floor for free; non-Carbon
   alternatives would require us to re-do the accessibility audit
   that Carbon's team has already done.

3. **Permissive licensing on the form, not the brand.** Carbon's
   token values are publicly documented; the IBM Plex font is
   permissively licensed; the *naming convention* is a documentation
   artefact, not a trademarked asset. The substrate references Carbon
   as a vocabulary source, not a brand. (See "What we do NOT import"
   below for the brand-specific elements explicitly excluded.)

Material was rejected because Google's design language carries
strong Google-product associations that conflict with brand
neutrality at the SMB level. Fluent was rejected for the same
reason against Microsoft. Spectrum and Polaris are tighter to their
parent brands (Adobe, Shopify) than Material or Fluent are to
Google or Microsoft, so even less neutral. Untitled UI was
considered as a primitive-only alternative; it ships under MIT-style
licensing and carries no brand association, but its accessibility
documentation is thinner than Carbon's. Future work may layer
Untitled UI as an alternative primitive bottom; v0.0.x ships Carbon
only.

## What is imported from Carbon

| Element | Imported as | Notes |
|---|---|---|
| Color primitives | `tokens/primitive.json` `color.{gray,blue,red,green,yellow}-NN` | Carbon's hex values used directly. |
| Type scale | `tokens/primitive.json` `typography.{productive,expressive}-0N` | IBM Plex Sans as the default font family; substituted per tenant via theme override. |
| Spacing scale | `tokens/primitive.json` `size.spacing-0N` through `spacing-13` | 8px grid; matches Carbon's. |
| Motion easing | `tokens/primitive.json` `motion.ease-{productive,expressive,entrance,exit}` | Cubic-bezier values from Carbon. |
| Duration scale | `tokens/primitive.json` `duration.{fast,moderate,slow}-0N` | Six steps from 70ms to 700ms. |
| Border radius | `tokens/primitive.json` `border.radius-0N` | 2px / 4px / 8px floor. |
| Focus ring | `tokens/primitive.json` `focus.ring` | 2px solid, blue-60 by default; WCAG 2.2 AAA conformant against any tenant background. |

## What is NOT imported from Carbon

| Element | Why excluded |
|---|---|
| Carbon Cloud themes (Carbon White, Carbon Gray 10, ...) | These carry IBM brand framing. The substrate ships `pointsav-brand` as the canonical PointSav theme; SMB customers ship their own. |
| Carbon React component implementations | The substrate is framework-agnostic; ships HTML+CSS+ARIA recipes. The customer's chosen framework consumes the recipe. |
| IBM logo and "Carbon" wordmark | Trademarked assets. Substrate references Carbon as an inspiration source by name, not as a re-brand. |
| IBM Plex font binary distribution | The font is permissively licensed (SIL OFL 1.1) but the substrate links to it as a font family declaration; customers self-host the font binary or substitute their own. |
| Carbon-specific component micro-interactions | The "feel" of a Carbon button (specific hover transition timing, ripple animation, ...) is not imported as a non-negotiable. The substrate's recipes use Carbon's motion primitives but compose them per-component. |

## Customer-fork behaviour at the primitive layer

Customers who fork the substrate inherit the Carbon-baselined
primitive layer as their starting floor. Overrides at the primitive
layer are discouraged but possible:

- A customer with strict brand-color requirements (e.g., a regulated
  financial-services SMB whose corporate colors are fixed by their
  charter) may add primitive entries (`color.brand-primary-50`, ...)
  alongside the Carbon imports. Their `themes/<their-brand>.json`
  then re-points semantic references to the new primitives.
- A customer whose accessibility target is below WCAG 2.2 AAA may
  override the focus ring style at the primitive layer. The
  substrate logs this at startup; the showcase displays a banner
  noting the override.
- A customer in a non-Latin-script jurisdiction may swap the type
  scale's font-family to a script-appropriate face (Noto Sans Thai,
  IBM Plex Arabic, ...) at the primitive layer. The token references
  carry through unchanged.

What customers should NOT do at the primitive layer:

- Rename Carbon's tokens (`spacing-01` → `xs`, ...) — the muscle
  memory benefit is the reason Carbon is the floor; renaming
  destroys it.
- Drop the focus ring or motion-respect declarations — these are
  WCAG-floor commitments the substrate does not retreat on.

## How AI agents should use this file

When generating tokens or evaluating brand-override choices for a
PointSav-tenant surface:

- Default to Carbon-naming-convention primitive references via
  `{color.blue-60}`, `{size.spacing-05}`, etc. — the substrate's
  DTCG bundle resolves these.
- Surface override decisions at the semantic layer, not the
  primitive layer. If a tenant brand needs `interactive-primary` to
  be `#7B2CBF`, override `themes/<brand>.json` to point at a new
  primitive `color.brand-purple-60`, not by editing
  `color.blue-60` directly.
- Use the type scale as the floor; do not introduce per-component
  font-size literals. If a component requires a non-standard size,
  add a new entry to the type scale and document the rationale.
- Honour the WCAG 2.2 AAA contrast floor unconditionally; refuse
  customer override requests that would drop below WCAG 2.2 AA at
  any token combination the substrate emits.

## References

- IBM Carbon Design System — https://carbondesignsystem.com/
- IBM Plex font (SIL OFL 1.1) — https://github.com/IBM/plex
- W3C Design Tokens Community Group format —
  https://design-tokens.github.io/community-group/format/
- WCAG 2.2 — https://www.w3.org/TR/WCAG22/
- Doctrine claim #38 — `~/Foundry/DOCTRINE.md` §III row 38
- Convention — `~/Foundry/conventions/design-system-substrate.md`
  §"IBM Carbon as the floor"
