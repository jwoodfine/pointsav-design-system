# Zoom-Tier Reveal Pattern

**Source:** research-zoom-tier-reveal-pattern.draft.md (Master workspace v0.1.94 / project-editorial, 2026-04-30)
**Cites:** gis.woodfinegroup.com (live reference), MapLibre GL JS docs, Sonnet sub-agent retail-mapping-UI-research 2026-04-30

---

## Pattern statement

A map view that holds many features benefits from a **zoom-tier reveal pattern** — at low zoom levels, only aggregate representations (cluster centroids) render; as the user zooms past a threshold, individual features reveal. The aggregates carry meaningful data (family distribution, cluster grade) that survives the threshold crossing. This is first-class data, not a rendering optimisation.

## Why this is novel

Industry-standard clustering (MapLibre native cluster source, Mapbox clusterRadius, Leaflet.markercluster, Supercluster) collapses points into a count-only marker — "73 stores in this area" — losing all per-feature semantics. Zoom-tier reveal preserves brand-family distribution semantics at every zoom level, aligning with leapfrog invention #1 (cluster-grade as first-class entity).

## Tier definitions (current GIS surface)

| Zoom | Layer | Visual |
|---|---|---|
| < 8.0 | Cluster centroids only | Brand-family ring; cluster-grade colour |
| 8.0–8.5 | Both layers (crossfade) | Centroids fade out; individual anchors fade in |
| ≥ 8.5 | Individual anchors only | Brand-family swatch per anchor |

## MapLibre implementation

```javascript
// Cluster centroids — show at low zoom, fade out above 8.5
map.addLayer({
  id: 'cluster-centroids',
  type: 'circle',
  source: 'co-locations',
  maxzoom: 8.5,
  paint: {
    'circle-opacity': [
      'interpolate', ['linear'], ['zoom'],
      8.0, 1.0,
      8.5, 0.0
    ]
  }
});

// Individual anchors — fade in above zoom 8
map.addLayer({
  id: 'individual-anchors',
  type: 'circle',
  source: 'places',
  minzoom: 8.0,
  paint: {
    'circle-opacity': [
      'interpolate', ['linear'], ['zoom'],
      8.0, 0.0,
      8.5, 1.0
    ]
  }
});
```

The 8.0–8.5 crossfade band is the key UX detail. A hard threshold at exactly zoom 8 creates a visible snap that breaks spatial continuity.

## Composition with other patterns

- **Country filter chips** — `flyTo` on chip select lands at zoom < threshold (e.g., zoom 4 for US-extent, 6 for ES-extent), keeping cluster-centroid view active; user zooms into a specific corridor.
- **Map side drawer** — clicking a cluster centroid `flyTo`s zoom 13 (above threshold), reveals individual anchors, opens drawer for cluster context.
- **Brand-family swatch** — cluster-centroid ring variant is the multi-family aggregate at zoom < threshold; inline chip / map marker variant is the per-anchor representation at zoom ≥ threshold.

## Threshold selection criteria

1. **Cluster spread** — at what zoom does the average cluster occupy ≥1 tile (individual anchors visually separable)?
2. **Density signal** — at what zoom does the cluster centroid carry more information than 4 individual swatches at the same screen position?
3. **Customer story** — at what zoom does the narrative shift from "global/regional pattern" to "this specific cluster"?

Current GIS surface: 8.0–8.5 crossfade band validated on 12-corridor / 41-anchor production data.

## Accessibility

- `prefers-reduced-motion: reduce` — collapse crossfade to instant swap; both representations remain usable.
- Screen-reader semantics — zoom-changes do not produce auditory events; user controls disclosure via interaction.
- Keyboard `+` zoom past 8 reveals individual anchors in the Tab order.

## Research trail

### Done

1. Reference implementation at gis.woodfinegroup.com confirmed operational: 12 cluster centroids at zoom < 8.5, 41 individual anchors at zoom ≥ 8, crossfade operational (v0.1.94).
2. MapLibre `minzoom`/`maxzoom` + `interpolate` paint expression documented as the recommended crossfade mechanism.
3. Industry comparison: Mapbox / Leaflet.markercluster / Supercluster all use count-only markers. This pattern is novel in preserving family-distribution semantics across the zoom threshold.
4. Operator demo at v0.1.94: 12-corridor view at zoom 2.6 shows cluster centroids legibly; clicking centroid flies to zoom 13 with individual anchors.

### Suggested

1. Validate the 8.0–8.5 crossfade band on production data at scale (target: 500+ corridors, 5,000+ anchors); band may need to widen at higher density.
2. Measure threshold-tier UX with eye-tracking — does the crossfade band cause split-attention?
3. Compare with industry-convergent clustering on identical data; document visual/semantic differences.
4. Audit 8.0/8.5 bounds against country-extent zoom levels — does any country sit awkwardly close to the threshold?
5. Test on `prefers-reduced-motion` users — does instant swap produce a usable experience?

### Open questions

1. Three-tier reveal (cluster centroid → cluster expansion → individual anchor) for dense clusters (100+ anchors) — needed, or does the 2-tier pattern hold?
2. Cluster centroid click: `flyTo` zoom 13 (current) vs `flyTo` zoom = threshold + 1 (preserves more spatial context)?
3. Per-layer threshold — should each map layer have its own threshold, or a single global threshold? Decision pending Phase-2 mobility-layer composition work.
