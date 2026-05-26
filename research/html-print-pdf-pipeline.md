# Design Research — HTML Print/PDF Pipeline

**Source:** design-research-html-print-pdf-pipeline.draft.md (totebox@project-bim, 2026-05-17)
**Language protocol:** DESIGN-RESEARCH
**Research trail:** 1 done · 0 suggested · 0 open questions
**Audience:** design-system
**ai_consumption_hint:** Canonical @page + Playwright PDF architecture for any HTML artifact that
must print or export to PDF. Reusable across all clusters. Three root causes of PDF pagination
failure documented with correct solutions. Reference implementation: `clones/project-bim/preview/build-pdf.mjs`.

---

## Summary

The correct architecture for producing print-quality PDFs from HTML slide decks is:
`@page { size: <exact dimensions>; margin: 0; }` with all whitespace owned by the slide
element, and PDF generation via headless Chromium (Playwright) rather than the browser print
dialog. This is the same pattern used by Google Slides, Reveal.js, Slidev, and Stripe Press.
The browser print dialog is not a build target.

Discovered and validated 2026-05-17 while fixing the project-bim `preview/*.html` slide decks.

---

## The problem with browser print dialog

The browser print dialog introduces three sources of non-reproducibility:

1. **Page size ambiguity.** `@page { size: landscape; }` inherits whatever paper the user
   (or system default) has configured — A4 vs Letter is a 0.27in width difference, enough
   to overflow content.
2. **Interactive state.** Headers/footers, background graphics, and margin presets must be
   manually toggled per operator, per session. Two operators printing the same HTML produce
   different PDFs.
3. **Responsive scale rules fire during PDF render.** Chromium computes CSS at the `@page`
   width (11in = 1056px) when generating the PDF. Any `@media (max-width: 1200px)` rule that
   applies a `transform: scale()` or margin adjustment to slides fires silently, shifting
   content across page boundaries. `transform: none !important` in `@media print` kills the
   transform but an unimportant `margin: -28px` in the responsive rule beats an unimportant
   `margin: 0` in the print rule by source order.

---

## Correct @page declaration

```css
@media print {
  @page {
    size: 11in 8.5in;   /* explicit dimensions, NOT the `landscape` keyword */
    margin: 0;           /* page owns no margin; slide owns all whitespace */
  }
}
```

**Why explicit dimensions:** `size: landscape` tells the user agent to rotate the
user-selected paper. `size: 11in 8.5in` forces US Letter landscape regardless of the print
dialog's paper selection. This is the difference between a reproducible artifact and a
user-dependent one.

**Why `margin: 0`:** The slide element is sized to match the page box exactly
(`width: 11in; height: 8.5in`). All internal whitespace (padding on `.slide-head`,
`.slide-body`, `.slide-foot`) is owned by the slide, not the page. Stacking `@page` margin +
slide internal padding + slide padding is triple-margining.

---

## Correct slide CSS in @media print

```css
@media print {
  /* Each slide IS one page. Same dimensions as the @page box. */
  .slide {
    width: 11in;
    height: 8.5in;
    box-shadow: none !important;
    margin: 0;
    transform: none !important;      /* defeat any responsive scale rule */
    page-break-after: always;
    break-after: page;
    page-break-inside: avoid;
    break-inside: avoid;
  }
  .slide:last-child {
    page-break-after: auto;
    break-after: auto;
  }
}
```

---

## Correct responsive media query scoping

Any responsive media query that scales or repositions slide elements **must be scoped to
`screen`**:

```css
/* WRONG — fires during Chromium PDF render at 1056px viewport */
@media (max-width: 1200px) {
  .slide { transform: scale(0.92); margin: -28px 0; }
}

/* CORRECT — screen-only; PDF render ignores it */
@media screen and (max-width: 1200px) {
  .slide { transform: scale(0.92); margin: -28px 0; }
}
```

Chromium's PDF generation pass runs CSS layout at the `@page` width. For a landscape letter
page, that is 1056px — below the typical 1200px responsive breakpoint. Without the `screen`
qualifier, the scale/margin rule fires, `transform: none !important` kills the transform in
`@media print`, but the margin survives by source order, drifting content across page
boundaries.

---

## Playwright PDF generator

File: `preview/build-pdf.mjs` (reference implementation in `clones/project-bim/preview/`).

The three critical flags:

```js
await page.pdf({
  printBackground: true,        // honour background colors / images
  preferCSSPageSize: true,      // use @page from the document, not API defaults
  displayHeaderFooter: false,   // no URL / page-number footer
  margin: { top: 0, right: 0, bottom: 0, left: 0 },
});
```

**`preferCSSPageSize: true`** is the key flag. Without it, Chromium uses the `format`
parameter (defaulting to Letter, which may or may not be the right size). With it, the
document's `@page { size: 11in 8.5in; }` declaration is authoritative.

**`printBackground: true`** is required for any slide deck with background colors (callout
boxes, zone-colored cells, chip backgrounds). Without it, all backgrounds are stripped.

**`displayHeaderFooter: false`** suppresses the default "page 1 of N / URL / date" footer
that the browser print dialog adds even when the slide deck has its own footer.

---

## CLI usage

```bash
# Single file
NODE_PATH=/home/jennifer/sandbox/working/ps-talking-points/node_modules \
  node preview/build-pdf.mjs preview/building-width-calculator.html

# All HTML files in the preview directory
NODE_PATH=… node preview/build-pdf.mjs all
```

Produces `<filename>.pdf` alongside the source HTML. Verified output:
`MediaBox [0 0 792 612]` = 11in × 8.5in per page.

---

## Checklist for any new HTML slide deck

- [ ] `@page { size: <W>in <H>in; margin: 0; }` — not the `landscape` keyword
- [ ] `.slide { width: <W>in; height: <H>in; transform: none !important; margin: 0; }`
- [ ] `page-break-after: always; break-after: page; page-break-inside: avoid; break-inside: avoid;` on each slide
- [ ] All responsive `@media (max-width: ...)` rules that touch `.slide` scoped to `screen`
- [ ] `print-color-adjust: exact !important` on `*` selector to force background printing
- [ ] Generate PDF via `build-pdf.mjs` (Playwright), not the browser dialog
- [ ] Verify `MediaBox` dimensions in output PDF match declared page size

---

## Applicability

| Artifact type | Example | Apply this pattern |
|---|---|---|
| Slide deck | `preview/*.html` | Yes |
| BIM inspection report | future `report-*.html` | Yes |
| GUIDE PDF | future HTML GUIDEs | Yes |
| Financial model summary | future proforma HTML | Yes |
| Token catalog export | `bim.woodfinegroup.com` print view | Yes |

The `build-pdf.mjs` script is generic — any HTML file path passed to it produces a PDF.
The CSS pattern is the contract; the script is the runner.

---

## Research provenance

- Opus deep-research agent, 2026-05-17: synthesised against Reveal.js, Slidev, Marp, Google
  Slides, and Stripe Press HTML-to-PDF pipelines. Identified `preferCSSPageSize: true`, the
  responsive-rule scoping bug, and the `@page size` ambiguity as the three root causes of the
  project-bim preview pagination failure.
- Reference implementation validated in production:
  `clones/project-bim/preview/build-pdf.mjs` commit `390c50b`.
