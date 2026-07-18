<div class="doc-header">
<span class="eyebrow">Components · Paper</span>
<div class="doc-header__badges">
<span class="badge">6 variants</span>
<span class="badge badge--brand">Tokens-backed (stale — see Provisional surfaces)</span>
<span class="badge">WCAG 2.2 AA target</span>
</div>
<p class="doc-header__lead">A print-first (WeasyPrint) proforma / projection dashboard document
register — letter-landscape, wide multi-period tables, a compliance line-number
gutter, and semantic total/subtotal/section-banner rows. V5 canonical spec
(post-design-audit) verified across the real Bencal proforma family. One of
six templates in the <a href="/paper/paper/overview">Paper</a> document-family
register.</p>
<div class="registry-note"><span>Rendered from</span> <code>components/financial-report-layout/recipe.json</code></div>
</div>

## What this template is

Financial Report Layout is a **print document register**, not a screen
widget. It describes the page geometry, rule-weight usage, typography, and
semantic-row treatment of compliance financial documents (proformas, income
statements, book valuations) as they print through
[WeasyPrint](/paper/paper/overview) to a letter-landscape PDF.

It is a **sibling of, not a synonym for,**
[Financial Statement (year-end)](/components/financial-statement-yearend/usage).
The two share the Paper pillar's rule-weight ladder and pagination discipline
but diverge deliberately:

| Axis | Financial Report Layout | Financial Statement (year-end) |
|---|---|---|
| **Page geometry** | Letter **landscape** | Portrait |
| **Density** | Up to **11 period columns** per wide table | Up to 3 |
| **Tone** | Section-banner fill only; total/subtotal are rule-weight, no fill | Pure black-on-white, zero fills |

Reach for this template when the deliverable is a forward-looking projection
or compliance financial statement that must show many periods side by side.
For a statutory, compliance-register year-end statement, use the year-end
sibling instead.

## This page supersedes a stale V1–V3 build

This component was first vaulted from V1–V3 of its source draft only
(commits `9c8155c`, `36295c3`, `0b71534`). The source draft continued to V4
(2026-07-16, tighter margins + anti-dead-space pagination) and V5 (2026-07-16,
canonical spec after a design audit) — neither ever landed here. **This page
reflects V5 as canonical**, correcting several claims the prior version of
this page made as final. If you have anything generated against the prior
version of this page, regenerate it — the font, the row-fill treatment, the
label-column width, and the line-number-gutter render mechanism all changed.

## Variants

The register defines six variants. Each is a real structural element of the
audited, print-verified Bencal document family — never invent a seventh.

| Variant | Role |
|---|---|
| **`masthead`** | Position-pinned draft stamp (fixes a V1 float-overlap bug) + V5 running header via CSS `string-set` + mandatory BCSC forward-looking footer. |
| **`wide-table-alignment`** | `table.wide` + `table-layout:fixed` so period columns align table-to-table within an aligned group; label column 24% (tightened from 25%). |
| **`semantic-rows`** | `tr.total` / `tr.subtotal` / `tr.section-banner` role classes — V5 replaces V1's tinted fills with horizontal rules only; `td.tbd` and `td.note` placeholder/prose treatments. |
| **`line-number-gutter`** | Compliance line-number column — **V5 corrects this to server-rendered** (V1–V3's JS injector never reached the actual WeasyPrint PDF); width 26px (was 32px). |
| **`section-block-pagination`** | `section.block` atomic wrapping + the `.tall` flow exception + repeating `<thead>`/`<tbody>` + the anti-dead-space rule against forced breaks on small sections. |
| **`chart-beside-table`** | `table.layout` for chart-beside-table / two-up bands — flexbox is banned for print in this family (WeasyPrint overlap bug). |

## Key CSS excerpts (V5 canonical)

Horizontal-rules-only row system — the single highest-impact change from the
prior vaulted version:

```css
th,td{border:0;border-bottom:1px solid #e3e3e3;padding:2px 6px;text-align:right;
  white-space:nowrap;font-variant-numeric:tabular-nums lining-nums}
th{font-weight:700;border-bottom:1.5px solid #999}
tr.subtotal td{font-weight:600;border-top:1px solid #aaa}
tr.total td{font-weight:700;border-top:2px solid #888;border-bottom:2px solid #888}
tr.section-banner td{background:#f2f4f7;font-weight:700;text-align:left}
```

Chart-beside-table / two-up — replaces flexbox:

```css
table.layout{width:100%;border-collapse:collapse}
table.layout>tbody>tr>td{border:0;padding:0 18px 0 0;vertical-align:top;
  text-align:left;white-space:normal;background:none;font-variant-numeric:normal}
```

Section pagination:

```css
section.block{break-inside:avoid}
table,tr,section.block{break-inside:avoid} h2,h3,h4{break-after:avoid}
```

Running header + page frame:

```css
@page{size:letter landscape;margin:1.05cm 1.1cm 1.2cm 1.1cm;
  @top-left{content:string(doctitle);font-size:8px;color:#999}
  @top-right{content:string(draftstamp);font-size:8px;color:#999}
  @bottom-center{content:counter(page) " / " counter(pages);font-size:8px;color:#999}}
@page :first{@top-left{content:none}@top-right{content:none}@bottom-center{content:none}}
```

## Token and CSS ownership

The canonical CSS for this family lives in project-proforma's own engine
(`tool-proforma-engine/src/report/bencal_v1_proforma.rs`, the `HEAD` const)
and in the hand-authored per-document `.html` files it produces alongside —
**not** in this vault. This vault holds the component's identity, structural
recipe, and documentation; the CSS stays authoritative at the source, the
same "CSS at the source, identity+docs here" division CIM (`legal-cim`) uses.
A divergence between the engine `HEAD` and the canonical CSS above is drift
for project-proforma to close, not a variant for this vault to document.

**The live DTCG token bundle is currently stale against this page.**
`dtcg-vault/paper/primitive.json` / `semantic.json` still register this
family's V1 values — `2cm`/`1.5cm` symmetric page margins (V5 uses four
distinct asymmetric values the current token shape can't represent), tinted
`row-total-bg`/`row-subtotal-bg` fills (V5 removes both entirely), and
`system-ui` as the body font (a WeasyPrint no-op; V5 uses Carlito). See
[Provisional surfaces](#provisional-surfaces-and-open-questions).

## Accessibility

Because this is a print artifact, accessibility here means **tagged-PDF
structure and print contrast**, not keyboard or focus behaviour:

- `scope="col"` on column headers, `scope="row"` on `td.lbl` cells (per the
  source draft's own ARIA notes).
- Non-colour signalling on emphasised rows is now **narrower** than this
  page previously claimed: V5 drops the uppercase text-transform and navy
  ink `tr.section-banner` previously carried. The current non-colour signal
  set is fill (banner only) + font-weight (all three roles) + rule weight
  (subtotal single / total double) — still never colour-only, but the exact
  mechanism changed.
- `td.lnum`/`th.lnum` are decorative (`aria-hidden`) regardless of how the
  gutter is rendered — unaffected by the V5 JS→server-render correction.
- WCAG 2.2 AA target. V5's removal of total/subtotal fills is a *stronger*
  non-colour-only guarantee than before, not a weaker one — there is
  no tint left on those two rows to fail a contrast check against.

## Print output and motion

Print-first static document. **As of V5 the line-number gutter is no longer
a screen-only feature** — it is server-rendered at generation time, so it now
appears identically in the WeasyPrint PDF and on screen. (Previously the
JS-injected gutter appeared on screen only, since WeasyPrint does not execute
JavaScript — the compliance line-number column was silently absent from the
actual delivered PDFs until V5's correction.)

## Provisional surfaces and open questions

- **Deep-linkable line numbers** — unresolved since V1; not addressed by any
  later update.
- **Five items V5 marks "deferred to project-design's build"**, carried
  forward verbatim as open work, not yet done: full `section.block` wrapping
  of every group; `td.note` classing of prose "Note" columns; migrating the
  Commissions document's `tr:last-child` total-hack to explicit semantic row
  classes; a formal `.stamp` element for engine-rendered docs (Commissions
  hardcodes its own; engine docs currently show doctitle only); `<thead>`/
  `<tbody>` emission for any table that spans pages (none do today).
- **Live token bundle mismatch** — flagged above under Token and CSS
  ownership; reconciling `dtcg-vault/paper/primitive.json`/`semantic.json`
  and `dtcg-vault/paper/paper.md`'s families table to V5 is a
  `DESIGN-TOKEN-CHANGE` requiring `master_cosign`, not performed by this
  page.
- **Font operational dependency** — Carlito requires `fonts-crosextra-carlito`
  on the render host (installed on the Foundry workspace VM 2026-07-16; not
  verified elsewhere).

## Related

- [Paper pillar — overview](/paper/paper/overview) — rule-weight ladder, geometry, and document-families table this register inherits (also stale against V5 — see Token and CSS ownership above).
- [Financial Statement (year-end)](/components/financial-statement-yearend/usage) — the portrait, black-on-white statutory sibling.
- [Legal CIM](/components/legal-cim/usage) — the other Paper family using the "CSS stays authoritative at the source" ownership split.
- [Interactive PDF Binder](/components/interactive-pdf-binder/usage) — the navigation-overlay register.
- [Tokens — Paper tier](/tokens#paper) — the seventeen leaf tokens backing this template (currently stale — see above).

<div class="doc-footer-meta">
<span>rendered from</span> <code>components/financial-report-layout/recipe.json</code>
<span class="doc-footer-meta__sep">&middot;</span>
<span>source research:</span>
<a href="/tokens#paper">research/financial-report-layout-token-map.md</a>
</div>
