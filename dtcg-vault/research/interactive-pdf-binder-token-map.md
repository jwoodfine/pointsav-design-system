---
schema: foundry-design-research-v1
component_or_token: interactive-pdf-binder
decision_type: token-consolidation
authored: 2026-07-13
authored_by: totebox@project-design
authored_with: claude-opus-4-8 (deep-read), claude-sonnet-5 (synthesis)
status: ratified
source: project-jennifer DESIGN-BUNDLE-Interactive-PDF-Binder-V1.md + tool-pdf-interactive/tool-pdf-interactive.py (canonical template, verified directly against the Python source, not just the draft's prose)
ai_consumption_hint: "Values here were pulled from the live Python constants, not the draft's own color table — one discrepancy found and corrected (a 7th color GREY_MID does not exist in code). This is a PDF-point-space component (612x792pt, origin bottom-left), a genuinely different rendering context from the CSS-print @page components elsewhere in the Paper pillar — do not force it to share paper.primitive.page.* geometry."
---

# Interactive PDF Binder Navigation — token consolidation rationale

Values in this component were extracted directly from `tool-pdf-interactive.py`'s own
Python constants (the authoritative source), not from the design draft's prose
description — one real discrepancy was found this way: the draft's color table lists a
7th token `GREY_MID` (`#666680`, described as "inactive entry subtitles"), but no
subtitle rows exist anywhere in the actual generator code. Dropped from this component's
token set rather than silently carried forward as a phantom value.

## Why this is a separate rendering context, not folded into paper.primitive.page.*

Every other Paper component in this consolidation is a CSS `@page`-based WeasyPrint
document. This component is generated directly in PDF point-space via `reportlab` +
`pypdf` — same physical units (points), genuinely different coordinate system (origin
bottom-left, not top-left; no `@page` box model). Kept as its own
`paper.primitive.pdf-nav.*` group rather than forced to share the CSS-print page
primitives, since the two are not interchangeable despite both using `pt`.

## Tool location and portability

The canonical template lives at
`project-jennifer/tool-pdf-interactive/tool-pdf-interactive.py` (258 lines) with
`README.md`/`README.es.md`. Seven filled-in production copies exist under
`project-jennifer/inputs/*/` for real Bencal/Agency/MOU/Mexico-Prospectus binders —
those remain business-admin artifacts and do not move. The canonical template itself is
self-contained (only `pypdf`/`reportlab` dependencies, no project-jennifer-specific
paths or business content) and ports to `pointsav-monorepo/tool-pdf-interactive/` with
low rework — the main generalizing step is lifting its top-of-file `CONFIG` block into
CLI arguments or a manifest file, so one installed tool can build any binder without
editing source.

A second, more-developed copy of this tool (676 lines, including a `find_home_anchor`
feature via `pdfplumber`) already exists committed directly at
`pointsav-monorepo`'s repository root — a real, pre-existing `repo-layout.md` violation
(no scripts allowed at repo root) predating this consolidation. That copy, not the
project-jennifer template, is the better base for the actual `tool-*` port (Step 6a of
this initiative), since it is already more feature-complete and already properly
licensed/committed within the monorepo; the project-jennifer template's design values
were used for this token consolidation since it is the cleaner, generalized reference
the design draft actually describes.

## Addendum 2026-07-21 — geometry realigned to shipped production binders

The 2026-07-13 consolidation above extracted values from the project-jennifer
*template*'s Python constants. On 2026-07-16, project-jennifer aligned its own 3
production binders (MX Prospectus, MOU, Agency Agreements) to the Bencal SPV1
*reference* layout and extracted a reusable engine — the template's own geometry
constants turned out to never have matched what any shipped binder actually renders.
Cross-checked against all 36 pdf-nav/pdf-binder tokens in
`dtcg-vault/exports/tokens.full.json`; colors and typography were already correct
(navy #002e63 pinned exact against the live reportlab RGB constant, not a naive
rounding), only geometry needed realignment:

| Token | 2026-07-13 (template) | 2026-07-21 (aligned, current) |
|---|---|---|
| `toc-entry-first-y` | 565pt | 595pt |
| `toc-entry-step` | 65pt | 48pt |
| `toc-entry-width` | 530pt | 468pt |
| `toc-num-x` | 64pt | 96pt |
| `toc-title-x` | 82pt | 114pt |
| `home-width` | 64pt | 54pt |
| `home-height` | 20pt | 14pt |
| `home-corner-radius` | 4pt | 3pt |

New primitives added for the ADOPTED grouped-TOC pattern (`toc-group-header` /
`toc-entry-child` variants, see recipe.json): `toc-child-dash-x` (120pt, itself amended
same day from an initial 140pt — see the component's oq history), `toc-header-to-child-step`
(26pt), `toc-parent-to-child-step` (36pt), `toc-active-marker-size` (7.2pt, a drawn rect
replacing an earlier pinned-glyph recommendation — glyph substitution rendering is
reader-dependent, not deterministic).

Source: `project-jennifer-20260716-dtcg-interactive-pdf-binder-pdf-nav-geom` (geometry),
`project-jennifer-20260717-adopted-interactive-pdf-binder-grouped-t` (grouped pattern +
token audit), `project-jennifer-20260717-amendment-to-the-adopted-grouped-toc-spe`
(child-dash correction + drawn-marker reversal). Two earlier messages in the same thread
(`project-jennifer-20260717-design-component-interactive-pdf-binder-`,
`project-jennifer-20260717-supersedes-msg-project-jennifer-20260717`) are superseded by
the ADOPTED message and were not used as a source here.
