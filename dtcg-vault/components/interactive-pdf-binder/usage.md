<div class="doc-header">
<span class="eyebrow">Components · Paper</span>
<div class="doc-header__badges">
<span class="badge">6 variants</span>
<span class="badge badge--brand">Tokens-backed</span>
<span class="badge">WCAG 2.2 AA target (print/PDF)</span>
</div>
<p class="doc-header__lead">A print-first navigation system for assembled multi-document
PDF binders on US Letter (612×792pt, origin bottom-left). One component, four
navigation surfaces — a slip-sheet table-of-contents cover, TOC entries (active,
inactive, and — new 2026-07-17 — grouped headers/children), and a HOME return button
stamped on every content page — that together turn a stack of concatenated source PDFs
into a document a reader can move through inside any PDF viewer.</p>
<div class="registry-note"><span>Rendered from</span> <code>components/interactive-pdf-binder/recipe.json</code></div>
</div>

## What it is

Interactive PDF Binder Navigation is not a DOM component. It is the design-system record
for the navigation layer that `tool-pdf-interactive.py` (reportlab + pypdf) stamps onto
an assembled binder of source PDFs. The recipe's `html`/`css` describe only the
design-system *preview* surface; the shipped artifact is a static PDF whose interactivity
lives entirely in PDF link annotations and the document outline.

Every value on this page — geometry, colour, type — is drawn from the canonical Python
constants in the generator, extracted directly rather than from prose, and consolidated
into the [Paper pillar](/paper/paper/overview) as the `paper.*.pdf-nav` / `pdf-binder`
token groups. See the [Paper tokens tier](/tokens#paper) for the leaf values.

This is the only member of the Paper document family that is genuinely *interactive*
within its viewer. The other five families are static CSS-print layouts:
[legal subscription agreement](/components/legal-subscription-agreement/usage),
[legal prospectus](/components/legal-prospectus/usage),
[legal agency suite](/components/legal-agency-suite/usage),
[financial report layout](/components/financial-report-layout/usage), and
[financial statement (year-end)](/components/financial-statement-yearend/usage).

## When to use

- **Assembling several source PDFs into one deliverable** — a binder of agreements,
  schedules, or statements that a reader must navigate between. The slip-sheet TOC gives
  each source document a cover and a jump target.
- **A binder that will be read on screen, in a PDF viewer.** The GoTo links and document
  outline are the point; a binder intended only for print does not need this layer.
- **When the reader needs to return to the index repeatedly.** The HOME button on every
  content page is the return path.

## When not to use

- **Do not use it for a single, authored document.** If there is nothing to bind, there
  is no TOC to generate — reach for the relevant CSS-print family instead.
- **Do not use it to restyle the source PDFs.** The generator overlays navigation; it
  does not reflow, re-tag, or re-typeset the documents it binds.
- **Do not treat the point-space geometry as CSS `@page` geometry.** This component is
  rendered in PDF point coordinates with a bottom-left origin — it deliberately keeps its
  own `paper.primitive.pdf-nav.*` group rather than sharing the CSS-print page primitives.

## The four navigation surfaces

The binder navigation is composed of four surfaces. TOC entries have an active and an
inactive form; grouped rows (new 2026-07-17) add a non-navigable header and an indented
child, giving six variants in total.

### 1 · Slip-sheet TOC cover

A generated cover page inserted before each source document. It carries a header title,
an organisation subtitle, a 1.5pt rule, an optional right-aligned draft/version label
(first sheet only), and an italic footer instruction. A single slip sheet holds **up to 8
TOC entries**; that ceiling is currently a hard limit in the generator, and now that
grouped rows exist at a different (26pt/36pt) pitch than plain rows (48pt), re-expressing
it as a vertical-space budget rather than a row count is under active reconsideration —
not yet decided (see Open questions, oq-2).

### 2 · TOC entry

One navigable row per bound document, in two states:

- **Inactive** — a navy number and title for a document other than the current one, with
  an invisible full-rect GoTo link to that document's slip sheet.
- **Active** — the row for the current document: a grey-light highlight rectangle, black
  text, and (amended 2026-07-17) a **drawn** 7.2×7.2pt filled marker — not a glyph. It
  carries no link, because it points at itself.

### 3 · Grouped TOC rows — header + child (new 2026-07-17)

Adopted as the standard treatment for slip sheets whose documents cluster into families
(e.g. a Subscription Agreement with Family/Friends and Accredited-Investor variants).
Two new rows:

- **toc-group-header** — a non-navigable division label: 11pt bold, Title Case, ink (not
  navy — it isn't a link). No box, no marker, no rule; grouping is proximity, not a drawn
  separator.
- **toc-entry-child** — an indented row nested under a header or under a clickable parent
  document. No number; an en-dash leads the title at `toc-child-dash-x`. Otherwise the
  same navy/ink/highlight rules as a plain TOC entry.

A document row can itself be a parent (its schedules are annexes to it, not siblings of
it) — see the `toc-entry-child` variant description for how its bookmark and link-rect
geometry differ from a plain group header's children.

### 4 · HOME return button

A 54×14pt navy rounded rectangle (3pt corner radius, amended 2026-07-17 — was 64×20pt/4pt
in an earlier draft, never matched by any shipped binder) with a white `HOME` label,
placed lower-right. It is stamped on every content page — never on a slip sheet — and
carries a transparent GoTo link back to page 0, top.

## Variants

| Variant | Surface | Description |
|---|---|---|
| **slip-sheet** | TOC cover | Generated cover preceding each source document: header title, org subtitle, 1.5pt rule, optional right-aligned draft label (first sheet only), italic footer instruction. Holds up to 8 TOC entries per sheet (under reconsideration, oq-2). |
| **toc-entry-inactive** | TOC entry | Navigable row for a non-current document: navy number + title, invisible full-rect GoTo link to that document's slip sheet. |
| **toc-entry-active** | TOC entry | Row for the current document: grey-light highlight rect, black text, drawn 7.2×7.2pt marker (not a glyph); no link (self). |
| **toc-group-header** | Grouped TOC | Non-navigable division label: 11pt bold Title Case, ink. Number at `toc-num-x`, label at `toc-title-x`. No box/marker/link/rule. |
| **toc-entry-child** | Grouped TOC | Indented child row: no number, en-dash at `toc-child-dash-x` (120pt), rect (98, y-7, 442, 22). Otherwise identical to a plain TOC entry. |
| **home-button** | Return button | 54×14pt navy rounded-rect (3pt radius) with white HOME label, lower-right placement. Stamped on every content page (never slip sheets); transparent GoTo link to page 0 top. |

## Coordinate space and geometry

The binder is generated in PDF point-space on US Letter, **612×792pt, origin
bottom-left** — not a CSS `@page` box model. All geometry comes from
`paper.primitive.pdf-nav.*`:

| Primitive | Token | Value |
|---|---|---|
| Page width | `{paper.primitive.pdf-nav.page-width}` | 612pt |
| Page height | `{paper.primitive.pdf-nav.page-height}` | 792pt |
| Content zone | `margin-left` / `margin-right` | 72pt–540pt |
| First TOC entry baseline | `toc-entry-first-y` | 595pt |
| TOC entry step (centre-to-centre) | `{paper.primitive.pdf-nav.toc-entry-step}` | 48pt |
| TOC entry height | `toc-entry-height` | 46pt |
| TOC entry width | `toc-entry-width` | 468pt |
| TOC number column x | `toc-num-x` | 96pt |
| TOC title column x | `toc-title-x` | 114pt |
| Grouped-TOC child dash x | `toc-child-dash-x` | 120pt |
| Header-to-child / child-to-child pitch | `toc-header-to-child-step` | 26pt |
| Parent-to-child pitch (clickable parent row) | `toc-parent-to-child-step` | 36pt |
| Active-row marker size | `toc-active-marker-size` | 7.2pt |
| HOME button width | `{paper.primitive.pdf-nav.home-width}` | 54pt |
| HOME button height | `{paper.primitive.pdf-nav.home-height}` | 14pt |
| HOME corner radius | `{paper.primitive.pdf-nav.home-corner-radius}` | 3pt |
| Slip-sheet rule stroke | `rule-stroke` | 1.5pt |

**Geometry realigned 2026-07-21** to the values project-jennifer's 3 production binders
(MX Prospectus, MOU, Agency Agreements) actually render — the prior values were an
earlier draft's own numbers, never matched by any shipped binder. See recipe.json's
`pdf-nav` primitive block description for the full source citation.

The 1.5pt slip-sheet rule is the **emphasis** step of the shared Paper
[rule-weight ladder](/paper/paper/overview) — the same 1.5pt used for cover rules and
summary-page borders elsewhere in the pillar.

## Colour and type tokens

Colour resolves through `paper.semantic.pdf-binder.*` to the `paper.primitive.color`
tier:

| Semantic token | Resolves to | Value | Role |
|---|---|---|---|
| `pdf-binder.toc-entry-inactive` | `pdf-nav-navy` | #002e63 | Inactive TOC number + title |
| `pdf-binder.toc-entry-active` | `ink` | black | Active-entry text |
| `pdf-binder.toc-entry-highlight` | `pdf-nav-grey-light` | #f5f5f5 | Active-entry highlight fill |
| `pdf-binder.home-button-fill` | `pdf-nav-navy` | #002e63 | HOME button rectangle |
| `pdf-binder.home-button-label` | `pdf-nav-on-navy` | #ffffff | HOME label |
| `pdf-binder.header-ink` | `ink` | black | Slip-sheet header title |
| `pdf-binder.supporting-ink` | `pdf-nav-grey-dark` | #4d4d4d | Subtitle + italic footer instruction |
| `pdf-binder.version-label-ink` | `pdf-nav-grey-label` | #737373 | Draft / version label |

Type is set in the PDF core-14 Helvetica stack (`Helvetica`, `Arial`) — no font
embedding required:

| Token | Size / weight | Applied to |
|---|---|---|
| `pdf-binder.binder-title-type` | 16pt bold | Slip-sheet header title |
| `pdf-binder.home-label-type` | 8pt bold | HOME label |
| `pdf-nav.subtitle` | 10pt regular | Org subtitle |
| `pdf-nav.toc-entry` | 11pt bold | TOC rows |
| `pdf-nav.footer` | 9pt regular, rendered italic (Helvetica-Oblique) | Footer instruction |
| `pdf-nav.draft-label` | 9pt regular | Draft / version label |

## Accessibility

This produces a **static PDF page**, so web-UI accessibility mechanisms — focus rings,
ARIA roles, keyboard tab order — do not apply. What applies is PDF-native accessibility,
and it is partial by design:

- **Navigation is `/GoTo` link annotations** plus a PDF document outline
  (`/PageMode /UseOutlines`), with `/DisplayDocTitle true` so viewers announce the
  document title rather than the filename.
- **Contrast is strong.** Navy #002e63 on white measures ~13:1, and white on navy ~13:1
  — both AAA. This is the print/PDF contrast target the recipe declares against WCAG 2.2
  AA.
- **Tagged-PDF reading order is not handled.** Source PDFs pass through **untagged** — the
  generator does not add Tagged-PDF structure, so reading-order conformance for assistive
  technology depends entirely on the tagging of the source documents. This is a known,
  open accessibility gap, not a solved property (see Open questions oq-3). Do not claim
  screen-reader conformance for a binder whose sources are untagged.
- **The active-row marker is graphics, not text (amended 2026-07-17).** The prior interim
  glyph marker lived in the text layer, so the active row was text-extractable; the drawn
  7.2×7.2pt rect is graphics-only, so "which tab am I on" now rests on shading and
  black-vs-navy alone for a screen-reader user. The active row remains indirectly
  identifiable (the only row on its sheet with no link annotation), but this is a real
  WCAG 1.3.1 trade-off, not yet resolved — see Open questions oq-5.

The artifact is static: no motion, no transitions.

## Open questions

Carried verbatim from the recipe so downstream consumers do not treat unresolved items as
settled:

- **oq-1 — phantom colour (RESOLVED 2026-07-21).** An earlier draft listed a 7th colour
  `GREY_MID` (#666680, "inactive entry subtitles") that does not exist in the canonical
  Python source. Confirmed 2026-07-16 by project-jennifer: no production instance renders
  subtitles. Stays dropped.
- **oq-2 — 8-entry ceiling.** The max-8-TOC-entries-per-slip-sheet limit is currently
  hard-coded. Evidence gathered 2026-07-16/17: a child row costs 26pt where a top-level
  row costs 48pt, so a row count can't express the real constraint (MOU renders 8 rows
  with ~4 rows of headroom at the aligned pitch). Re-expressing this as a vertical-space
  budget is recommended but the actual formula is still undecided.
- **oq-3 — Tagged-PDF conformance.** Reading-order conformance for assistive technology is
  unhandled; source PDFs pass through untagged.
- **oq-4 — navy hex rounding (RESOLVED 2026-07-21).** The RGB constant `(0, 0.18, 0.39)`
  computes to ~#002f63 by a naive calculation; confirmed 2026-07-16 against the live
  reportlab source that the actual rendered value is #002e63 exactly. Stays pinned.
- **oq-5 — active-marker WCAG 1.3.1 trade-off (new 2026-07-17, undecided).** The drawn-rect
  active marker (see Accessibility above) is not text-extractable, unlike the interim
  glyph it replaced. A hidden text marker layered behind the box is the suggested fix if
  this is addressed — not implemented in this pass.
- **oq-6 — reference-binder bug, informational only.** The Bencal SPV1 *reference* binder
  and the bundle engine both carry a pre-existing child-rect bug — `(98, y-25, 442, 24)`,
  entirely below the text baseline — distinct from this recipe's corrected
  `(98, y-7, 442, 22)`. All 3 of project-jennifer's rebuilt production binders use the
  corrected value; the reference binder itself was not touched.

<div class="doc-footer-meta">
<span>part of</span> <a href="/paper/paper/overview">Paper pillar</a>
<span class="doc-footer-meta__sep">&middot;</span>
<span>tokens:</span>
<a href="/tokens#paper">paper.semantic.pdf-binder</a>,
<a href="/tokens#paper">paper.primitive.pdf-nav</a>
<span class="doc-footer-meta__sep">&middot;</span>
<span>rendered by</span> <code>tool-pdf-interactive.py</code>
</div>
