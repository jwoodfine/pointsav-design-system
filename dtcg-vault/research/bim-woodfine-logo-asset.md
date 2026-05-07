# Woodfine Logo Asset — Branding Spec Notes

**Source:** design-research-asset-woodfine-logo.draft.md (project-bim, 2026-05-06)  
**Status:** Research record — operator action pending (SVG extraction to BIM showcase static/)

---

## Issue

The inline SVG Woodfine wordmark in `app-orchestration-bim/src/render.rs` function
`woodfine_wordmark_svg()` was authored from memory without reference to the canonical asset.
The aspect ratio, typography sizing, and hash placement may differ from the canonical spec.

## Canonical Asset Locations

| Asset | Path |
|---|---|
| Full wordmark SVG | `customer/woodfine-media-assets/assets/logo/wf-logo_V1.svg` |
| Spec YAML | `customer/woodfine-media-assets/tokens/design/wf-logo-spec_V1.yaml` |
| Signet only | `customer/woodfine-media-assets/assets/logo/wf-signet_V1.svg` |
| Wordmark (root) | `customer/woodfine-media-assets/ASSET-WORDMARK-WOODFINE.svg` |

## Technical Spec (from wf-logo-spec_V1.yaml)

| Property | Value |
|---|---|
| ViewBox | `0 0 144 36` |
| Primary colour | `#111827` (Woodfine Slate, dark context default) |
| Wordmark | "WOODFINE" in Geist Bold 11px |
| Descriptor | "CAPITAL PROJECTS" in Geist Medium 6.5px |
| Structural hashes | 10.164 × 1.2702 px at specified coordinates |
| Aspect ratio | 4:1 |

## Recommended Deployment Target

The canonical SVG should be placed at:
```
pointsav-monorepo/apps/app-orchestration-bim/static/images/woodfine-logo.svg
```

The `woodfine_wordmark_svg()` function in `render.rs` should be replaced with an `<img>` tag
referencing `/static/images/woodfine-logo.svg`, eliminating the inline SVG string that must be
maintained manually.

## Operator Action Required

Master extraction of the SVG data from `wf-logo_V1.svg` to the target path above is pending.
Until the canonical SVG is extracted to the BIM showcase static directory, the render.rs inline
SVG remains in place.

## Open Questions

1. Confirm bSDD URI once buildingSMART publishes stable office space type entries, or create a
   PointSav-hosted bSDD dictionary entry.
