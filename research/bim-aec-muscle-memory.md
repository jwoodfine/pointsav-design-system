# AEC muscle-memory — universal interface conventions

Every AEC practitioner who has used Revit, ArchiCAD, BricsCAD, or
Bonsai (formerly BlenderBIM) carries a learned interface vocabulary.
The Building Design System adopts that vocabulary by default. New
users who are AEC-native have zero learning curve on basic
navigation; learning is reserved for the parts of `app-workplace-bim`
that are genuinely new (the flat-file vault, the code-as-composable-
geometry overlay, the BIM + lease register convergence).

## What every AEC tool does the same

(From sub-agent BB.4 Bonsai deep-dive plus sub-agent A's prior-art
review, both 2026-04-28.)

| Convention | Across | Building Design System equivalent |
|---|---|---|
| Spatial tree on the left | Revit Project Browser; ArchiCAD Tree View; Bonsai Outliner; BricsCAD Drawing Explorer | `SpatialTree` (left rail) |
| Properties panel on the right | Revit Properties; ArchiCAD Info Box; Bonsai Properties Editor sidebar | `PropertiesPanel` (right rail) |
| Tree expands to storey level by default, NOT to spaces | All four | `SpatialTree[default-expand="storey"]` |
| Toolbar at top of viewport | All four | `Toolbar` (top) |
| Status bar at bottom (coords + selection) | All four | `StatusBar` (bottom) |
| NavCube top-right of viewport | Revit, BricsCAD; absent in Bonsai (Blender N-panel handles it) | `Viewport3D__navcube` (top-right) |
| Section plane control | All four | `SectionPlane` |
| Filter / visibility controls | All four | `SelectionFilter` |
| Type library / family browser | Revit, ArchiCAD, Bonsai | `TypeBrowser` |

## What `app-workplace-bim` should mirror from Bonsai

(BB.4 specifically.)

- **Storey-level default expansion of the SpatialTree.** Every AEC
  practitioner navigates at storey level first. Auto-expanding into
  the spaces level is overwhelming; it adds visual noise without
  matching mental model.
- **PropertiesPanel as a sidebar, not a modal.** Selection-sensitive
  panel that updates in place; not a popup window.
- **Pset / Qto grouping.** Bonsai groups Pset_* property sets into
  named sections; the Building Design System mirrors that.

## What `app-workplace-bim` should DELIBERATELY NOT inherit from Bonsai

(BB.4 specifically.)

- **Bonsai uses Blender's Outliner panel as the SpatialTree.** That
  works for power users in Bonsai's host environment but it is a
  Blender-host artifact, not a Bonsai design decision worth carrying
  forward. The Outliner is a general-purpose scene-graph viewer
  with no purpose-built expand/collapse, no search-by-space-name,
  no floor-plan thumbnail preview. `app-workplace-bim` builds a
  dedicated SpatialTree widget instead.
- **Blender's modal mode-switching workflow.** Edit-mode / Object-mode
  / Sculpt-mode is a Blender concept that is invisible in pure
  authoring tools (Revit / ArchiCAD do not expose modal mode-switching
  to the user). Don't carry forward.
- **Blender's keymap — Numpad-1/3/7 for ±X/±Y/±Z views.** Most laptops
  ship without numpads. Use the convention Revit and BricsCAD use:
  number keys 1-6 along the top row.

## Property managers — the persona that doesn't exist in Bonsai's market

(From the strategic source's "property-manager BIM gap" diagnosis.)

Bonsai targets architects/designers. PointSav's
`app-workplace-bim` targets the FM operator persona that current
authoring tools do not address — the property manager who needs to
look up a wall's fire rating, attach a work order to a door, link a
lease to a space, or check whether a maintenance schedule has
expired. The Building Design System adds three workflows that have
no Bonsai equivalent:

1. **WorkOrder linking.** Attach a work order to an IFC element
   (per-element YAML sidecar carries the work-order GUID + status +
   assignee).
2. **Lease linking.** Attach a lease record to an IfcSpace
   (sidecar references the lease entity in the
   project-bookkeeping vault).
3. **Sensor overlay.** Live MQTT-backed sensor readings overlaid
   on the relevant element in `Viewport3D`.

These are workplace-unique components and not part of the v0.0.1
universal-component scope; v0.0.2+.

## References

- `~/Foundry/.claude/sub-agent-results/A-bim-design-system-prior-art-2026-04-28.md`
- `~/Foundry/clones/project-bim/.claude/sub-agent-results/BB.4-bonsai-interface-deepdive-2026-04-28.md`
- `~/Foundry/BIM_Buildable Architecture.md` — strategic source
- Bonsai (formerly BlenderBIM) — https://bonsaibim.org
