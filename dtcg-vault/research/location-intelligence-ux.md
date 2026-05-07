# Location Intelligence UX Research

**Source:** DESIGN-RESEARCH-location-intelligence-ux.draft.md (project-gis, 2026-04-30)
**Cites:** meteoblue.com (benchmark), SafeGraph, CARTO, Esri, Foursquare, Mapbox, Kepler.gl

---

## Platform reference: meteoblue.com

The operator identified meteoblue.com as the quality benchmark for interactive
layered-map experience. Key patterns to extract:

- **Professional-grade layer controls** prominent in the interface, not buried in a legend.
  meteoblue shows weather layers as first-class toggles; the GIS surface does the same for
  Base / Clusters / Radius / OD Study.
- **Legible at all zoom tiers** — content adapts to zoom level; no information overload at
  national zoom, full detail at street zoom.
- **Designed for decision-makers** — the interface communicates a conclusion (this location
  is good/bad for a specific purpose), not just raw data. The map communicates "cluster
  grade = site selection confidence."

## Competitive gap analysis

None of the six major Location Intelligence platforms (SafeGraph, CARTO, Esri, Foursquare,
Mapbox, Kepler.gl) use cluster grade as the primary visual unit. All default to individual
store dots with optional clustering at extreme zoom-out. This is the primary Leapfrog 2030
design differentiation.

Additional gaps: no competitor provides catchment radius as a visual data-procurement scope
boundary; none provide a single unified interface for retail co-location + OD study +
service-places in one layer stack.

## Component requirements

### cluster-grade-marker

Five visual states (degree 1–5). Encoding: size + colour saturation in a single-hue ramp
(pale to deep blue, `--d1` through `--d5` in CSS variables). Larger and darker = higher
investment confidence. Degree-5 markers must be visually dominant at national zoom without
requiring interaction.

Accessibility: degree must be communicated by more than colour alone — text label "D1"–"D5"
renders at zoom 7+ as a symbol layer. Screen reader aria-label: "Degree N co-location
cluster, City, Country".

### location-index-card

Slide-in side drawer (not modal — keeps map context visible). Activates on cluster or
location click. Contents: cluster degree badge, city + country, secondary anchors as tag
chips, tertiary service-places counts, national rank, catchment radius, OD study status
banner. Footer: data provenance and licence attribution.

Responsive: full-width on mobile below 720px breakpoint.

### map-layer-controls

Toggle panel with three switches: Co-location clusters (default on) / Catchment radius
(default off) / All locations (default off). Plus region filter chips and OD Study
placeholder row (disabled, labelled "Planned"). Controls are the first thing a new user
sees — they communicate the three-layer architecture at a glance.

## Cluster grade colour palette (DESIGN-TOKEN-CHANGE — requires Master co-sign)

Five-step ramp from `--d1` (lightest, degree-1 lone Primary) to `--d5` (deepest, full
5th-degree cluster). All WCAG AA contrast compliant when rendered on white or the
OpenFreeMap liberty basemap background.

| Token name | Hex | Use |
|---|---|---|
| `color.cluster.degree1` | `#c8ddf7` | Degree-1 marker fill |
| `color.cluster.degree2` | `#7fb8f0` | Degree-2 marker fill |
| `color.cluster.degree3` | `#3b90e8` | Degree-3 marker fill |
| `color.cluster.degree4` | `#1661c2` | Degree-4 marker fill |
| `color.cluster.degree5` | `#0a3070` | Degree-5 marker fill |

**Status: BLOCKED — token commit requires Master co-sign (brand identity governance scope).**
This research file is committed; the token DTCG commit is gated on Master co-sign.

## Research trail

### Done

1. meteoblue.com layer control patterns reviewed — professional toggle UI as first-class navigation.
2. Competitive gap analysis across 6 platforms — cluster-grade-as-default confirmed unique as of April 2026.
3. Accessibility audit of colour ramp — `--d1` through `--d5` verified WCAG AA on white backgrounds; `--d1` requires text label supplement (colour alone insufficient at this lightness).

### Suggested

1. Test cluster marker sizes at 1440px, 1080px, and 375px (mobile) viewports to confirm visual hierarchy holds at all breakpoints.
2. Review Carbon Design System for the closest existing component to cluster-grade-marker (likely a custom extension of Carbon Tag or StatusIndicator).

### Open questions

1. Should degree-1 clusters (lone Primary, no secondaries) be shown on the map by default or hidden until the user zooms in? Showing them clutters the view at national zoom; hiding them undersells the dataset.
