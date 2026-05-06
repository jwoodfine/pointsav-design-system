---
schema: foundry-design-research-v1
component_or_token: cluster-grade-marker, location-info-card, chain-search-input
decision_type: pattern-extraction
authored: 2026-05-06
authored_by: project-gis Task (sourced); refined by project-design Task
authored_with: claude-sonnet-4-6
status: staged
originating_cluster: project-gis
brand_voice_alignment: [direct, precise, professional]
accessibility_targets: [wcag-2-2-aa]
ai_consumption_hint: "Two reusable component candidates extracted from a GIS map deployment. chain-search-input (typeahead highlight filter) and location-info-card (structured inspector panel) are general enough for any data-dense surface. Read §Component extraction candidates before generating either component."
open_questions:
  - id: oq-1
    question: "Should clearing a chain filter also reset the inspector panel to overview mode, or should the panel retain the last-clicked cluster state?"
    status: open
  - id: oq-2
    question: "On mobile, should the cluster inspector use a tab bar (Cluster / Selected) rather than a stacked layout to manage vertical space competition?"
    status: open
---

# GIS UI design research — chain search + bento box (2026-05-06)

Two interface patterns shipped in the GIS map sprint: a retailer chain
search/highlight and a restructured cluster inspector (bento box). Both
address the same operator need — making the map legible as a lookup
tool, not only as an exploration surface.

---

## 1. Chain search (light-up filter)

### Problem

A map showing 4,237 undifferentiated clusters gives no way to isolate
brand-level pattern without clicking every cluster. Density is visible
at overview zoom; brand coverage is not.

### Solution

A typeahead input in the panel header filters by brand name. Matching
clusters glow amber with a ring; all others dim to 10% opacity.

Interaction flow:

1. Type a brand name → dropdown shows canonical names matching the
   string
2. Select → `activeChainFilter` set, `reapplyChainHighlight()` fires
3. All clusters containing a matching location (in `hw_list` or
   `wh_list`) receive full opacity and an amber stroke ring
4. Non-matching clusters dim to 10% opacity
5. `×` button clears the filter and restores uniform display

### Implementation pattern

The filter evaluates MapLibre's `['in', chainId, ['get', 'hw_list']]`
expression — a substring match against the JSON-encoded array stored in
the tile property. No tile reload; no API call; purely paint-layer
manipulation.

A dedicated `nodes-highlight` layer (circle, amber stroke, no fill)
toggles visible/hidden. This leaves the base `nodes` layer color logic
unmodified.

Key data structures:

- `CHAIN_DISPLAY_NAMES` maps chain IDs to display names
  (`"home-depot-ca"` → `"Home Depot"`)
- `BRAND_CHAINS` reverses the map: `"Home Depot"` → all regional chain
  IDs
- The filter expression checks all chain IDs for a brand in a single
  `['any', ...]` expression

### Design tokens needed

- `--color-highlight-amber`: `#F59E0B` (ring stroke on matching
  clusters)
- `--opacity-dim`: `0.10` (non-matching clusters)
- `--opacity-active`: `0.88` (matching clusters)
- Typeahead dropdown: inherits panel surface token; 180 px max-height;
  scrollable

**Open question oq-1:** Should clearing the filter also reset the
inspector panel to overview mode, or should the panel retain the
last-clicked cluster state?

---

## 2. Bento box information hierarchy

### Problem

The original inspector panel led with raw data (score, tier) before
establishing geographic context. An operator viewing an unfamiliar
cluster had no immediate orientation before encountering a numeric
grade.

### Operator brief

> "Region Market first, then Market Grade and Co-location Score, then
> Anchor Location, then Nearby Services, then Retailer Info at the
> bottom."

### Revised hierarchy

```
1. Market Region          — geographic anchor (bold, brand-primary navy)
2. Market Grade · Score   — tier badge + score_final / 1000 (flex row)
3. Anchor Location        — primary retail node (pill + sub-entities)
4. Co-Tenants             — HW + WH chain pills
5. Nearby Services        — medical / academic counts
6. sel-el block           — cycling selected-element detail
```

The `sel-el` block inverts the usual "inspector leads with the clicked
item" convention. The cluster's grade and anchor are always the primary
read; individual element detail is secondary context. This reflects the
operator's workflow: grade and anchor first, then drill into any dot.

**Open question oq-2:** On mobile, the `sel-el` block competes for
vertical space with the cluster-level content. A tab bar (Cluster /
Selected) may be preferable to a stacked layout on narrow viewports.

---

## Component extraction candidates

Two components identified as reusable across PointSav surfaces beyond
GIS:

**`cluster-grade-marker`** — tier badge (T3/T2/T1) and score display.
Currently inline HTML inside `showClusterDetail()`. Suitable for list
views, export tables, and print layouts.

**`location-info-card`** — the inspector panel. Currently a `<div
id="inspector">` with inline innerHTML. Should be a structured
component with named slots: region, grade, anchor, co-tenants,
services, element-detail. Slot-based design makes the component usable
without GIS-specific data.

Both components are candidates for `dtcg-vault/components/` once the
open questions above are resolved and a cross-surface use case is
confirmed.
