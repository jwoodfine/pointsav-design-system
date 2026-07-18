---
schema: foundry-design-research-v1
component_or_token: financial-report-layout
decision_type: token-consolidation
authored: 2026-07-13
updated: 2026-07-18
authored_by: totebox@project-design
authored_with: claude-opus-4-8 (deep-read), claude-sonnet-5 (synthesis, 2026-07-13 + 2026-07-18 V4/V5 update)
status: ratified
source: project-totebox DESIGN-COMPONENT-financial-report-layout.draft.md (V2, originating_cluster project-proforma) + project-proforma DESIGN-TOKEN-CHANGE-wcp-finance-bundle.draft.md + BRIEF-bencal-proforma-engine-recapitalization.md; V4/V5 update sourced from the same draft's own 2026-07-16 appended sections
ai_consumption_hint: "V5 CANONICAL SPEC as of 2026-07-18 — read the 'V4/V5 Update' section below before using anything above it. Several claims below (system-ui font, tinted total/subtotal fills, JS-injected line numbers, 'statement theme is provisional') are superseded. Still true: this is a SIBLING of financial-statement-yearend, not the same register — different page geometry (landscape vs. portrait), different density (up to 11 period columns vs. 3)."
---

# Financial Report Layout (Proforma / Projection Dashboard) — token consolidation rationale

This component's CSS was extracted verbatim from a real, delivered WCP V2 proforma
report — print-tested, genuinely production-grounded. Its companion `wcp.finance.*`
token bundle is a separate concern: `BRIEF-bencal-proforma-engine-recapitalization.md`
states the underlying Rust engine work (`forecast_statements.rs`'s classic
`statement` theme) is "planned but deliberately not yet implemented," so the
statement-theme's specific values are provisional, not equally final to the
dashboard theme's extracted CSS.

## Why this is a separate recipe, not a variant of financial-statement-yearend

The operator's "one recipe per document family" rule keys on genuine document family,
not just tone. This family and financial-statement-yearend disagree on:

- **Page geometry**: this family is letter landscape (`1.5cm 2cm 1.5cm 1.5cm` asymmetric
  margins); the yearend statement is letter portrait (1in symmetric). This is the
  sharpest divergence — they do not share a page-geometry primitive.
- **Density**: up to 11 period columns (label 22-25%) vs. 3 value columns (label 55%).
- **Tone**: tinted 3-saturation blue semantic-row fills + navy section-banner text vs.
  pure black-on-white, zero fills.
- **Nil glyph and page-number placement**: em-dash `—` / `@bottom-right` here, vs.
  en-dash `–` / `@bottom-center` Notes-only for the yearend statement — both deliberate
  per-family choices, confirmed not to be drift to reconcile.

## What genuinely is shared with financial-statement-yearend

Print-first single self-contained HTML + inline `<style>` (no framework/build),
WeasyPrint as the render target, `table-layout: fixed`, parenthetical negative
formatting, tabular-nums, and the single-rule-then-double-rule subtotal/total
convention (this family's statement theme: 0.75pt then 1pt+3pt-double; the yearend
statement: 0.5pt then 1pt+3pt-double) — modeled as the shared
`paper.primitive.rule.*` group both families draw from.

## Open items (as of 2026-07-13 — see V4/V5 Update below for current status)

The line-number gutter (32px, Courier New, JS-injected) is a dashboard/screen-only
feature — it does not render in WeasyPrint output and is entirely absent from the
statement theme; it is not a print-domain token, kept as a documented recipe variant
only. The statement theme's exact serif stack and column split remain provisional
until the proforma engine work referenced above actually lands.

---

## V4/V5 Update (2026-07-18) — canonical spec reconciliation

This component was vaulted 2026-07-13 from only V1–V3 of its source draft
(commits `9c8155c`, `36295c3`, `0b71534`). The source draft gained a V4
(2026-07-16, tighter margins + anti-dead-space pagination) and a V5
(2026-07-16, canonical spec after a Fable design audit) that were never
brought into this vault — no commit existed for either until this update.
This section records what changed, grounded in a direct read of the full
draft.

### Key findings

- **The "statement theme is provisional" gate above has structurally
  lifted.** The 2026-07-13 entry framed a second "statement theme" as gated
  on `BRIEF-bencal-proforma-engine-recapitalization.md`'s "planned but
  deliberately not yet implemented" Rust engine work. V4/V5 describe that
  same engine (`tool-proforma-engine/src/report/bencal_v1_proforma.rs`) as
  live, having its `HEAD` const corrected for drift (V4) and then brought to
  a single canonical CSS spec verified in WeasyPrint across the real Bencal
  family — SPV1, Management, ShareCapital, and Commissions (V5). There is no
  longer a "dashboard theme (real) vs. statement theme (provisional)" split
  to describe — V5 is one canonical spec the engine and every hand-authored
  document must match.
- **Font: `system-ui` was a silent no-op, not a real choice.** The V1–V3
  research above justified `system-ui` as avoiding a web-font dependency.
  V5 corrects this: WeasyPrint silently falls back to DejaVu Sans on
  `system-ui` — the font choice never actually took effect in the delivered
  PDFs. Carlito (Calibri-metric) is the corrected choice, with
  `font-variant-numeric:tabular-nums lining-nums` now mandatory on every
  cell. Operational dependency: `fonts-crosextra-carlito` on the render
  host (installed on the Foundry workspace VM 2026-07-16 per the draft; not
  independently verified for any other render host).
- **Row fills: V5 removes them from total/subtotal entirely.** The V1
  three-saturation blue-fill system (`#eef2f7`/`#f5f7fa`/`#e3edf7`) is gone
  for total/subtotal as of V5 — "horizontal rules only... the single
  highest-impact aesthetic change" per the audit. `tr.section-banner` is now
  the *only* filled row, and even it drops the V1 navy ink (`#1a2a44`) and
  uppercase treatment.
- **The line-number gutter was never actually reaching the compliance PDF.**
  The most consequential correction in V5, and it corrects this file's own
  prior framing directly. V1–V3 treated `td.lnum` as a deliberate
  JS-injection design choice. But WeasyPrint does not execute JavaScript —
  so on every one of these compliance documents, rendered through the
  stated primary render target, the line-number gutter that exists
  specifically to support "line 42" style compliance review was silently
  absent from the actual delivered artifact the whole time V1–V3 were live.
  V5's fix: emit `lnum` cells at generation time (a doc-wide running
  counter) instead of via client-side JS. Width also tightened 32px → 26px.
  This is a correctness fix, not a style preference.
- **Page margin token shape mismatch, not just a stale value.** The live
  `page-margin-inline`/`page-margin-block` token pair assumes a symmetric
  (or at most block/inline) margin. V5's `@page` margin is
  `1.05cm 1.1cm 1.2cm 1.1cm` — four independently-set values. No two-token
  pair can represent this correctly; reconciling it requires either four
  leaf tokens or a single composite margin token, a decision for whoever
  runs the follow-on `DESIGN-TOKEN-CHANGE`, not decided here.
- **Anti-dead-space is now a hard rule, narrowing V2's own advice.** V2
  introduced `.page-break-before`/`.page-break-after` as a general tool. V4
  narrows this: forcing a break on a *small* section strands it alone on an
  otherwise-empty page. The corrected guidance relies on `break-inside:avoid`
  + `break-after:avoid` to pack pages, reserving forced breaks for
  statements that must legally/visually start fresh.
- **Flexbox is banned for print in this family — a real, reproduced bug.**
  V4 found WeasyPrint overlapping a pie chart onto its adjacent data table
  under nested flexbox. V5 applies the fix (`table.layout`) and confirms it
  renders correctly in the audited ShareCapital render.
- **Live DTCG token bundle is now stale against V5, not just against this
  file's 2026-07-13 predecessor.** `dtcg-vault/paper/primitive.json` and
  `semantic.json` still carry the V1 values this section describes as
  superseded, and `dtcg-vault/paper/paper.md`'s document-families table
  likewise still states "2cm inline, 1.5cm block" / "system-ui." None of
  these three files were edited by this update — reconciling registered
  token *values* is a `DESIGN-TOKEN-CHANGE` requiring `master_cosign` per
  this repo's own intake checklist; this file flags the mismatch rather
  than silently fixing it.
- **What genuinely didn't change.** The core cross-table alignment
  mechanism (`table-layout:fixed` + shared label width), the
  semantic-class-not-inline-style principle, letter-landscape as the
  compliance print standard, and the `.tall`-flow / repeating-`<thead>`
  pagination scheme from V3 all carry forward unchanged into V5.

### Research trail (this update)

**Done (+9):** read the full source draft V1–V5 directly; confirmed no
V4/V5 vault commit existed; confirmed the statement-theme provisional gate
is now stale; confirmed the `system-ui` no-op and Carlito correction;
confirmed V5's fill removal and section-banner ink/uppercase drop; confirmed
the JS line-number gutter never reached the actual delivered PDF under
WeasyPrint; confirmed the live token bundle still encodes pre-V4/V5 values;
confirmed the page-margin token pair cannot represent V5's four asymmetric
values; confirmed the flexbox-overlap bug and its `table.layout` fix are
reproduced/verified findings; confirmed V1–V3's structural decisions remain
the component's foundation, unaffected by V4/V5.

**Open questions (carried forward, 1):** should `td.lnum`/`th.lnum` be
semantically addressable (an `id` per line) for deep-linkable "line 42"
review references, or remain purely decorative? Unresolved since V1.

**Deferred (per V5's own list, 5):** full `section.block` wrapping of every
group; `td.note` classing of prose columns; migrating the Commissions
document's `tr:last-child` total-hack to explicit semantic classes; a
formal `.stamp` element for engine-rendered docs; `<thead>`/`<tbody>`
emission for any table that spans pages.

**Not performed by this update (flagged, not silently done):** no edits to
`dtcg-vault/paper/primitive.json`, `semantic.json`, or `paper.md` —
reconciling live token values to V5 is a `DESIGN-TOKEN-CHANGE` requiring
`master_cosign`. No resolution of the page-margin token shape mismatch.
