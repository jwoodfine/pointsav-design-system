# BIM token taxonomy — eight primitives

The eight token primitive categories were validated against IFC 4.3
entity hierarchy by sub-agent A research, 2026-04-28. The original
operator draft (Materials / Elements / Spaces / Systems / Connections
/ Codes / Performance / Identity) was refined to match canonical IFC
classification conventions:

| Primitive | IFC Anchor | Notes |
|---|---|---|
| **SPATIAL** | `IfcSpatialElement` | Site / Building / Storey / Space hierarchy |
| **ELEMENTS** | `IfcBuiltElement` | Walls, slabs, columns, beams, doors, windows, roofs, stairs, railings, coverings |
| **SYSTEMS** | `IfcDistributionElement` | MEP — pipes, ducts, cables, flow terminals, distribution systems |
| **MATERIALS** | `IfcMaterial` + bSDD | Single materials + layer sets + constituent sets + Pset_Material* |
| **ASSEMBLIES** | `IfcElementAssembly` | Hierarchical compositions; furnishings; geographic site features |
| **PERFORMANCE** | `IfcPropertySet` + `IfcQuantitySet` | Pset_*Common templates + Qto_*BaseQuantities |
| **IDENTITY+CODES** | `IfcClassificationReference` + `IfcConstraint` | Uniclass / OmniClass / MasterFormat + IfcConstraint for jurisdictional rules |
| **RELATIONSHIPS** | `IfcRel*` | Spatial containment, aggregation, openings, classification association, material association, property attachment, junction connectivity |

## Refinements vs. operator's original draft

- **Spaces → SPATIAL.** Renamed to avoid collision with the singular
  IfcSpace; the category covers the full IfcSpatialElement hierarchy
  (Site / Building / Storey / Space).
- **Connections → RELATIONSHIPS.** IFC's vocabulary is `IfcRel*`;
  using the IFC noun avoids divergence between the design-system
  vocabulary and IFC's own.
- **Identity + Codes merged.** Both anchor on
  `IfcClassificationReference`. The operator's original Identity
  category and Codes category turned out to share the same IFC
  entity backbone, so the merger produces a cleaner taxonomy without
  losing semantic distinction (an Identity reference is a
  classification reference into a published taxonomy; a Code
  reference is a classification reference into a jurisdictional
  rule-publication taxonomy — same shape, different namespace).

## Classification floor — Uniclass 2015

Per sub-agent A research, Uniclass 2015 is the recommended
classification floor. It is published by NBS (UK), free to use,
openBIM-recognised, with eleven primary tables: Co (Complexes), EF
(Elements/Functions), Ss (Systems), Pr (Products), Ma (Materials),
Pm / PM (Project Management), Ro (Roles), FI (Forms of Information),
Ac (Activities), SL (Spaces/Locations), PC (Project Costs), PE
(Project Elements).

Uniclass plays the role in project-bim that Carbon-baseline plays in
project-design's META-substrate: the floor every element receives by
default, with deployment-specific classifications (OmniClass /
MasterFormat / city-specific) layering on top.

## Eighteen components

| Category | Components |
|---|---|
| **Universal AEC (10)** | SpatialTree, PropertiesPanel, Viewport3D, ViewNavigator, Toolbar, StatusBar, SelectionFilter, TypeBrowser, SectionPlane, AnnotationLayer |
| **Console-unique (4)** | BimGuidSearch, BimAuditLog, BimDashboard, BimExportPanel |
| **Workplace-unique (4)** | MaterialsBrowser, TypeEditor, ClashDetector, VersionHistory |

The 10 universal AEC components share `data-mode="workplace"` /
`data-mode="console"` prop variants. Console-unique and
workplace-unique components are surface-specific and do not appear in
the other surface.

## Component-recipe pattern

Each component lives at
`pointsav-design-system/components/bim-<name>/` with three files:

- `recipe.html` — semantic markup (no framework). The reference
  rendering that every host integration matches.
- `recipe.css` — namespaced CSS using the component's BEM class
  prefix. No framework dependency.
- `aria.md` — accessibility contract: roles, labels, keyboard
  navigation, mode-prop behaviour, don'ts.

Host frameworks (Yew / Leptos / vanilla TS) integrate by mounting the
recipe markup, attaching event listeners, and respecting the mode
prop and the aria contract. The recipe is the contract; the host
implementation is the realisation.

## v0.0.1 component coverage

- ✅ `bim-spatial-tree`
- ✅ `bim-properties-panel`
- ✅ `bim-viewport-3d`
- 🚧 `bim-view-navigator`, `bim-toolbar`, `bim-status-bar`,
     `bim-selection-filter`, `bim-type-browser`,
     `bim-section-plane`, `bim-annotation-layer` (next session)
- 🚧 `bim-guid-search`, `bim-audit-log`, `bim-dashboard`,
     `bim-export-panel` (console-unique; v0.0.2 once
     `service-buildings` ships its element index)
- 🚧 `bim-materials-browser`, `bim-type-editor`,
     `bim-clash-detector`, `bim-version-history` (workplace-unique;
     v0.0.2)
- 🚧 `bim-code-rs1` — the City-Code-as-Composable-Geometry
     showcase component (v0.0.2 alongside Woodfine BC RS-1
     encoding)

## References

- `~/Foundry/.claude/sub-agent-results/A-bim-design-system-prior-art-2026-04-28.md` (414 lines, April 2026)
- IFC 4.3 / ISO 16739-1:2024 — https://www.iso.org/standard/84123.html
- Uniclass 2015 — https://www.thenbs.com/our-tools/uniclass
- buildingSMART Data Dictionary — https://www.buildingsmart.org/users/services/buildingsmart-data-dictionary/
