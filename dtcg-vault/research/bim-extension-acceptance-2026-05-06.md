---
schema: foundry-design-research-v1
component_or_token: tokens/bim, components/bim-*, research/bim-*
decision_type: extension-acceptance
authored: 2026-05-06
authored_by: project-design Task
authored_with: claude-sonnet-4-6
status: accepted
originating_cluster: project-bim
brand_voice_alignment: [direct, precise, professional]
accessibility_targets: [wcag-2-2-aa]
ai_consumption_hint: "project-design META-substrate formally accepts the BIM extension structure proposed by project-bim. Read this file for path conventions and the license flag before generating any BIM-scoped work."
---

# BIM extension — structural acceptance (2026-05-06)

Source: `project-bim/.agent/drafts-outbound/design-index.md`
(DESIGN-RESEARCH, authored 2026-04-28, project-bim Task).

project-design META-substrate accepts the BIM extension as landed on
`cluster/project-bim` branch of `pointsav-design-system`. The
acceptance covers structure, token taxonomy, component set, and
research files as described below.

---

## Path structure — open question resolved

**Decision:** co-resident namespacing (current default) is accepted.

```
tokens/bim/                   — BIM-semantic DTCG token primitives
components/bim-*/             — BIM-specific component recipes
research/bim-*.md             — BIM design philosophy and taxonomy
tokens/uniclass-2015.dtcg.json — Classification floor (Uniclass 2015)
```

**Rationale:** Co-resident namespacing keeps the DTCG bundle coherent.
A DTCG consumer (Figma Variables import, Tailwind config, Style
Dictionary build) walking `tokens/` gets generic primitives and BIM
primitives in a single tree traversal. A top-level `bim/` directory
would require every consumer to know about two separate roots.

The `bim-` prefix on components and `bim-` prefix on research files
is sufficient isolation. When the BIM extension promotes to canonical
via Stage 6, the `tokens/bim/` sub-directory and `bim-` namespaces
make the BIM content discoverable without fragmentation.

project-bim Task: no path changes needed before Stage-6 promotion.

---

## Token taxonomy — accepted

Eight DTCG primitive files cover the IFC 4.3 entity hierarchy:

| File | Coverage |
|---|---|
| `tokens/bim/spatial.dtcg.json` | IfcSite / IfcBuilding / IfcBuildingStorey / IfcSpace / IfcFacility |
| `tokens/bim/elements.dtcg.json` | IfcWall, IfcSlab, IfcColumn, IfcBeam, IfcDoor, IfcWindow, IfcRoof, IfcStair, IfcRailing, IfcCovering |
| `tokens/bim/systems.dtcg.json` | IfcDistributionElement family |
| `tokens/bim/materials.dtcg.json` | IfcMaterial + LayerSet + ConstituentSet + Pset_Material* |
| `tokens/bim/assemblies.dtcg.json` | IfcElementAssembly + IfcGeographicElement + IfcFurnishingElement |
| `tokens/bim/performance.dtcg.json` | Pset_*Common + Qto_*BaseQuantities |
| `tokens/bim/identity-codes.dtcg.json` | IfcRoot.GlobalId + IfcClassificationReference + constraint metadata |
| `tokens/bim/relationships.dtcg.json` | IfcRel* relationship types |
| `tokens/uniclass-2015.dtcg.json` | Uniclass 2015 classification floor (11 tables, April 2026) |

The IFC 4.3 anchoring is correct. The Uniclass 2015 co-resident token
gives any consumer a standardised classification vocabulary without a
separate lookup call.

---

## Component set — accepted

Three universal AEC components landed at v0.0.1:

| Component | Notes |
|---|---|
| `components/bim-spatial-tree/` | Default-expand to storey level per AEC convention (BB.4 rationale) |
| `components/bim-properties-panel/` | Pset / Qto grouping per Bonsai convention |
| `components/bim-viewport-3d/` | xeokit embed; AGPL-3.0 scope (see §License flag below) |

Fifteen additional components are queued for v0.0.2 onwards per
project-bim's planned_design_drafts list. No blocking concerns.

---

## Architecture decisions — noted

The three architecture decisions (xeokit over @thatopen for
double-precision rendering; Tauri 2.10 IPC pattern; IfcOpenShell
LGPL-3.0 dynamic invocation) are accepted as project-bim cluster
scope. project-design does not own these decisions — they live in the
cluster manifest and research files on `cluster/project-bim`.

---

## License flag — forwarded to Master

The draft surfaces: combined xeokit (AGPL-3.0 workspace clause) +
EUPL-1.2 work distributes as **AGPL-3.0**. Specifically,
`app-workplace-bim` (the component containing the xeokit WebGL
surface) is AGPL-3.0; `app-orchestration-bim` and standalone services
that do not link xeokit remain EUPL-1.2.

This is a workspace-tier licensing fact. project-design forwards it to
Master for BCSC posture review and `factory-release-engineering`
acknowledgement. project-design does not make this call unilaterally.

---

## Response to project-bim

Accept as-is. Path structure confirmed: no changes before Stage-6
promotion. Response relayed via Master outbox (cross-cluster writes go
through Master per session-role rules).
