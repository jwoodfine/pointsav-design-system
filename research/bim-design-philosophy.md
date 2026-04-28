# BIM design philosophy

The Building Design System is the AEC counterpart of IBM Carbon. Eight
token primitive categories anchored to IFC 4.3 entity hierarchy,
eighteen component recipes covering universal AEC interface
conventions plus surface-specific variants, and a Uniclass 2015
classification floor that plays the role Carbon-baseline plays in the
META-substrate.

The design stance is structural: PointSav's existing architectural
commitments — flat-file storage, open standards, Rust + Tauri,
offline-first, EUPL-licensed, seL4-hardened — are not stylistic
preferences. They are the precise constraints that make five
hyperscaler weaknesses into customer-visible differentiators. The
Building Design System makes those structural commitments visible to
every architect, engineer, and property manager who opens
`app-workplace-bim` for the first time and finds the panel layout,
keyboard shortcuts, and naming conventions they already know from
Revit, ArchiCAD, BricsCAD, and Bonsai.

## Five hyperscaler-incompatible capabilities

(From the strategic source `~/Foundry/BIM_Buildable Architecture.md`,
April 2026.)

1. **Asset-anchored BIM.** The digital twin is signed with the land
   title. Travels with the property deed when ownership transfers.
   Multi-tenant SaaS cannot offer this without breaking the tenancy
   model.
2. **Offline-capable BIM for field use.** Basements, rooftops,
   air-gapped defence facilities, healthcare campuses with strict
   data residency. ACC, Tandem, iTwin Experience cannot work offline
   by construction.
3. **Vendor-obsolescence-survivable BIM.** Buildings live 50+ years;
   Revit's file format lasts three. The flat-file archive (IFC-SPF +
   BCF 3.0 + IDS 1.0 + COBie + glTF + CityJSONSeq + per-element YAML
   sidecars) is readable for decades after any specific vendor is
   gone.
4. **IoT integration directly into the BIM archive.** Per-element
   YAML sidecars ingest sensor readings via local MQTT broker. Data
   never leaves the owner's premises. No sensor-count-based token
   charges.
5. **Convergence of BIM + lease register + financial ledger** in one
   portable archive. PointSav's existing app-workplace family
   (memo, presentation, proforma) extends to BIM. The Totebox
   Archive becomes the first data architecture where a building's
   legal, financial, spatial, and operational identity are one
   portable artifact. Multi-tenant cloud cannot commingle these by
   construction.

## The compositional-first framing for codes

Twenty years of prior art exists in post-design code validation
(Solibri, CORENET X, Archistar, AEC3PO, Symbium). PointSav's framing
is compositional-first: cities publish building codes as composable
BIM design tokens (bSDD dictionaries + IDS 1.0 constraints + IFC
geometric exclusion-zone fragments), and the designer assembles
inside pre-constrained envelopes from the first placement. Violations
become geometrically impossible by construction. The Carbon analogy
is exact: developers don't draw a button and then run an
accessibility checker — they compose from Carbon tokens that are
already accessible by construction.

This framing is the leapfrog (proposed Doctrine claim #41).

## Relationship to project-design's META-substrate

project-design owns the META-substrate per Doctrine claim #38: Carbon
baseline + DTCG vault + AI-readable research backplane. project-bim
adds the BIM-SEMANTIC layer on top: 8 BIM token categories anchored
to IFC 4.3 + 18 component recipes + Uniclass 2015 classification
floor + the City-Code-as-Composable-Geometry overlay model.

This is the same shape as project-orgcharts consuming the
META-substrate as a downstream consumer. project-bim is downstream
consumer for the META-substrate but is OWNER of the Building Design
System sub-substrate. New BIM components flow project-bim →
project-design via cluster-design-draft-pipeline (DESIGN-* drafts in
this cluster's `.claude/drafts-outbound/`, picked up by
project-design Task at sweep time).

## References

- `~/Foundry/BIM_Buildable Architecture.md` — strategic source (96 lines, April 2026)
- `~/Foundry/.claude/sub-agent-results/A-bim-design-system-prior-art-2026-04-28.md`
- `~/Foundry/.claude/sub-agent-results/B-bim-city-code-as-geometry-2026-04-28.md`
- `~/Foundry/.claude/sub-agent-results/C-bim-regulatory-acceptance-2026-04-28.md`
- `~/Foundry/clones/project-bim/.claude/manifest.md` — cluster manifest
- Doctrine claim #38 — Design System Substrate
- Doctrine claim #40 (proposed) — Flat-File BIM Substrate
- Doctrine claim #41 (proposed) — City Code as Composable Geometry
