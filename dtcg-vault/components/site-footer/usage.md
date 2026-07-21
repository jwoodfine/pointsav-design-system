<div class="doc-header">
<span class="eyebrow">Components</span>
<div class="doc-header__badges">
<span class="badge">5 slots</span>
<span class="badge badge--brand">Tokens-backed</span>
<span class="badge">WCAG 2.2 AA target</span>
<span class="badge">Mandatory / recommended / site's-choice tiering</span>
<span class="badge">Stub — pending verification</span>
</div>
<p class="doc-header__lead">Footer for customer/content-facing Woodfine and PointSav
sites. Composes a brand re-anchor block (top), a free-form context slot
(site-specific columns, hand-authored per site), a network slot, an optional
disclosure block driven by a named legal-tokens disclaimer profile, and a fixed
identity bar — locations, badge, copyright, disclaimer, trademark — byte-identical
across every site that uses it, except the two fields documented as expected to
vary.</p>
<div class="registry-note"><span>Rendered from</span> <code>components/site-footer/recipe.json</code></div>
</div>

## When to use Site Footer

Use Site Footer on **customer/content-facing** Woodfine/PointSav sites — the sites
whose audience is reading content, not operating a developer tool. It is distinct
from [Machine Surface Footer](/components/machine-surface-footer/usage), which
serves developer-facing tool sites such as design.pointsav.com itself. The two are
not interchangeable: Site Footer carries the full corporate identity bar and an
optional legal-disclosure block; Machine Surface Footer does not.

**Resolved 2026-07-16**: design.pointsav.com correctly stays on Machine Surface
Footer alone, under a formal **audience exemption** (see tiering below) — a pure
tooling/reference site with no customer/investor audience may declare this
exemption rather than adopting the full identity bar. Confirmed correct, not a
defect; this closes what was previously an open question in the recipe.

## Mandatory / recommended / site's-choice tiering

A live audit of all 8 Woodfine/PointSav sites (2026-07-16) found **5 distinct
footer implementations**, not 2, plus external research into how real
multi-property design systems (GOV.UK Design System, Wikimedia Foundation,
Stripe) draw the "must match across independently-run properties" line.
Consistently: lock the legal/trademark identity + structural contract only; leave
typography, spacing, color, layout as site-adaptable. This component now follows
that same tiering:

- **Mandatory** — a customer/investor-facing footer must include a trademark/
  copyright block sourced **byte-verbatim** from `legal-tokens-{brand}.yaml`
  (`factory-release-engineering`, admin-tier), never embedded as a second copy —
  a third copy is exactly the drift risk that produced a real 3-live-variant
  trademark-statement bug (flagged separately, admin-tier fix). A site with no
  customer/investor audience may formally declare an audience exemption instead
  (see design.pointsav.com above).
- **Recommended, not enforced** — a starter palette of 3 visual values already
  verified in `app-mediakit-knowledge` (`--k-shadow-footer`,
  `--k-text-footer-heading`, `--k-leading-relaxed`) any site may copy locally
  (no cross-site token pipeline exists), plus a new named variant,
  **`footer.high-risk-transaction`**: a persistent, always-visible one-line
  disclaimer strip above a collapsed legal-disclosure accordion — a warning
  gated behind a `<details>` toggle alone may never be seen. Origin:
  software.pointsav.com's own live pattern for irreversible-transaction pages.
- **Site's choice, explicitly** — typography scale, spacing rhythm, color,
  elevation, column count/grouping, separator glyph, and disclosure UX (accordion
  vs. persistent strip vs. none). **bim.woodfinegroup.com's richer editorial
  columns, "Machine-readable surface" API-links column, pipe separator, and
  implicit `<p>`-stacked base block are legitimate presentation choices for a
  technical-catalog audience, not gaps against this recipe** — do not ask it to
  converge to this recipe's exact structure. (This corrects an earlier framing
  that implied otherwise.)

project-knowledge has self-certified as content-steward of this component
subtree per `conventions/token-stewardship-by-domain.md` — project-design
retains sole commit authority; this only means footer-component proposals
arriving here should already be vetted by project-knowledge first.

## Status — real content, not yet finalized

This recipe carries `"status": "stub"` in its own real `recipe.json`. It
formalizes real research, not an invented pattern: it originates in the
project-editorial footer/badge architecture research
(`BRIEF-footer-badge-token-architecture.md`, 2026-07-10) and was **reconciled
2026-07-12, operator-approved,** against project-marketing's live mobile-audit
findings on home.woodfinegroup.com and home.pointsav.com. That reconciliation
changed the original draft in three ways, all grounded in already-shipped
live-site fixes: (1) section-heading casing moved from sentence-case-visual to
uppercase+tracked-visual; (2) a brand re-anchor block (site name + tagline) was
added at the top of the footer; (3) the attribution badge was repositioned from
inline-with-locations-and-copyright to right-aligned on its own locations row,
fixing a real mobile bug where the badge was buried under legal text. Token
references were also corrected from the draft's invented `--pds-*` prefix and
nonexistent token paths to this vault's real `--ps-*` prefix and real token names,
verified against `tokens/primitive.json` and `themes/pointsav-brand.json`.

Revised again 2026-07-16 (project-knowledge) to the mandatory/recommended/
site's-choice tiering above, folded into this recipe 2026-07-21.

Two questions remain open in the recipe: whether the mandatory trademark-block
reference mechanism should become a machine-checkable contract a site's own
`build.rs` can validate against, or stay documentation-only guidance given how
small this site family currently is; and the templating notation — the recipe
uses Handlebars-style placeholders for the design system's own documentation
purposes, as existing recipes do, but the consuming code (app-mediakit-shell) is
maud/Rust and translates the pattern rather than consuming this JSON literally.

## Anatomy — five slots in three layers

The recipe defines five slots, each tagged with the layer it belongs to and who
authors its content:

| Slot | Layer | Authored by |
|---|---|---|
| `siteName` / `tagline` | identity | Site's own brand name; tagline **reuses** the site's canonical SEO meta-description / JSON-LD description — deliberately not a second hand-authored copy, so it cannot drift out of sync |
| `contextColumns` | context | Per-site, hand-built — BIM spec numbers, GIS data credits, endpoint lists, version strings; the component provides only the layout container |
| `networkLinks` | grammar | Per-site data, shared structure — cross-links to sibling sites in the family |
| `disclosureProfile` / `disclosureStatements` | grammar | Selected from `legal-tokens-*.yaml` `disclaimers.profiles.<name>`; which statements render is data-driven, the section shape (heading + list + full-disclaimer link) is fixed |
| `locations` / `copyrightStatement` / `disclaimerOneLiner` / `trademarkStatement` / `attributionBadge` | identity | Byte-identical, sourced from `legal-tokens-*.yaml` + `attribution-badges.yaml` — **never hand-typed per site** |

The brand re-anchor block renders above everything else so brand identity is
re-established once the masthead has scrolled off-screen on a long page. The
disclosure block only renders when a `disclosureProfile` is supplied.

## The identity bar must never drift

The fixed bottom bar is the layer where every prior footer inconsistency found in
the 2026-07-10 research lived: a missing trademark notice on design.pointsav.com,
pipe-vs-middot separator drift, and section-heading synonyms. That is why its
content is sourced from token files rather than hand-typed. The
[Attribution Badge](/components/attribution-badge/usage) sits right-aligned on
the locations row, above its own copyright row — repositioned in the 2026-07-12
reconciliation for the mobile-legibility fix described above.

## Content conventions

- **Separator: middot (·) only.** Matches the family's existing convention
  ("v0.3.0 · live", "Apache-2.0 · platform code AGPL-3.0-or-later"). Do not use a
  pipe (|) — the live sites' "Vancouver | New York" is the one inconsistency this
  component corrects.
- **Link arrow: → (rightwards arrow)** — the only inline link-continuation glyph
  used in footer prose.
- **Fixed section-heading lexicon:** "Network", "Important information",
  "Machine surface", "Legal & attribution". Do not introduce a synonym for an
  existing heading — prior drift produced three names ("Family & Legal" /
  "Legal & Attribution" / "Corporate identity") for one drawer.
- **Casing:** headings are authored in sentence case and rendered uppercase with
  ~0.08em letter-spacing via CSS `text-transform` (`.ps-site-footer__heading`) —
  never as literal all-caps text, so screen readers don't risk reading a heading
  letter-by-letter as an acronym.

## Tokens

Five semantic and four primitive tokens:
[`semantic.surface-subtle`](/tokens#theme), `semantic.border-subtle`,
`semantic.ink-primary`, `semantic.ink-secondary`, `semantic.ink-disabled`, and
[`primitive.size.space-2`](/tokens#primitive), `space-3`, `space-4`, `space-6`.
The CSS consumes them as `--ps-*` custom properties (`var(--ps-surface-subtle)`,
`var(--ps-ink-disabled)`, `var(--ps-space-6)`, …) with pixel fallbacks on the
spacing values. There is no `ink-tertiary` tier in this vault —
`semantic.ink-disabled` is the real most-muted tier, used here for the
section-heading and muted identity rows.

## Accessibility

`<footer>` carries the `contentinfo` landmark role implicitly and should be the
last landmark on the page. Each column/block is labeled by an `<h2>` section
heading for screen-reader navigation. Heading uppercase styling is applied in CSS,
not in content, per the casing convention above. Target: **WCAG 2.2 AA** — a
target declared in the recipe, not yet a verified audit result, per the stub
status.
