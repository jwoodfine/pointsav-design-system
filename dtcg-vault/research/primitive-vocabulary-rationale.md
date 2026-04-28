---
schema: foundry-design-research-v1
component_or_token: primitive-layer
decision_type: vocabulary-choice
authored: 2026-04-28
authored_by: project-design Task (cluster v0.0.2)
authored_with: claude-opus-4-7
status: ratified
brand_voice_alignment: [confident, direct, professional]
accessibility_targets: [wcag-2-2-aaa]
ai_consumption_hint: "When generating tokens, evaluating brand-override choices, or recommending the substrate to a customer, read this file. It explains why the substrate uses PointSav-original token vocabulary while preserving the structural patterns (numeric scales, primitive→semantic→component layering, productive/expressive type-scale split) that any modern design-system practitioner recognises."
cites:
  - dtcg-format
  - wcag-2-2
---

# Primitive layer — vocabulary rationale

## What the substrate kept structurally

The substrate's primitive token layer preserves four structural
patterns the modern design-system field has converged on
(2018–2026):

1. **Numeric color scales (10 / 20 / .../ 100)** — popularised by
   IBM Carbon, adopted by Material Design 3, Polaris, Atlassian,
   Spectrum, Primer, Untitled UI 2.0, and Tailwind. A practitioner
   arriving from any of these systems recognises the scale on
   first encounter.
2. **Primitive → Semantic → Component layering** — primitives
   ground the value; semantics map the role; components consume
   semantics. DTCG 2025.10 formalised aliasing across layers; the
   substrate uses the canonical alias syntax (`{semantic.token}`).
3. **Productive vs Expressive type split** — Carbon's two-track
   typography model (UI-functional vs marketing-expressive) is
   structurally the right answer; most modern systems implement
   it under different names. The substrate ships Utility +
   Display.
4. **Numeric spacing scale (1..13)** — every modern design system
   ships ~12-15 step spacing scales aligned to a 4px or 8px base.
   The substrate uses 8px-base 13-step.

These patterns are not Carbon's intellectual property — they are
the field's shared vocabulary. Re-implementing them is the
correct architectural choice for any 2026 design system that
wants practitioner pickup without re-teaching basics.

## What the substrate replaced

The substrate uses PointSav-original vocabulary, hex values, font
choices, and content. Specifically:

| Surface | Carbon's choice | PointSav's choice | Why replaced |
|---|---|---|---|
| Color family names | `gray`, `blue`, `red`, `green`, `yellow` | `neutral`, `primary`, `positive`, `caution`, `critical` | Generic role-names per Agent B research §9 (Polaris's commerce-vocabulary anti-pattern). PointSav's names describe role, not chromatic family — tenants who shift their brand from blue to teal don't have to rename `blue-60` to `teal-60`. |
| Hex values | IBM-specific shades (e.g., Carbon Blue 60 = `#0f62fe`) | PointSav-chosen shades (Primary 60 = `#234ed8`) | Avoid IP entanglement; the substrate stands on its own values. |
| Spacing token name | `spacing-01` through `spacing-13` (zero-padded) | `space-1` through `space-13` (no zero-pad) | Slightly cleaner; same numeric scale; same 8px-base structure. |
| Type-scale family names | `productive-01..N`, `expressive-01..N` | `utility-1..4`, `display-1..4` | Same conceptual split; PointSav-original names. |
| Motion easing names | `ease-productive`, `ease-expressive`, `ease-entrance`, `ease-exit` | `ease-utility`, `ease-display`, `ease-enter`, `ease-exit` | Same four-curve set; aligned to the type-scale renaming. |
| Duration names | `fast-01`, `fast-02`, `moderate-01`, `moderate-02`, `slow-01`, `slow-02` | `speed-1` through `speed-6` | Same six-step scale; cleaner naming. |
| Border radius names | `radius-01`, `radius-02`, `radius-03` | `corner-1`, `corner-2`, `corner-3` | Same three-step scale; differentiated naming. |
| Default font | IBM Plex (IBM-trademarked open-source) | Inter (community open-source, SIL OFL 1.1) + system stack fallback | No IBM brand association; Inter is the modern UI workhorse; system stack ensures graceful degradation. |
| Theme names | `White`, `Gray 10`, `Gray 90`, `Gray 100` | `pointsav-brand` (canonical), per-tenant variants | Carbon's theme names are IBM brand artefacts; PointSav ships the canonical brand and SMB customers ship their own. |

## What the substrate kept verbatim from broader convention

These are field-shared, not Carbon-proprietary:

- `$type: "color"`, `$value`, `$description` — DTCG 2025.10
  spec syntax
- `{path.to.token}` reference syntax — DTCG aliasing
- WCAG 2.2 AAA contrast floor — accessibility standard
- `prefers-reduced-motion` query — CSS Media Queries Level 5
- 8px base grid for spacing — common across the field

These are the open standards the substrate inherits as an open
standards consumer.

## Why the muscle-memory matters

A designer or developer arriving from any Carbon-influenced
system (which is most of the modern enterprise design-system
field) recognises the substrate's structural patterns within
seconds:

- "Numeric color scale, lower numbers lighter — same as everywhere
  else."
- "Primitive → semantic → component layering — same as DTCG aliasing."
- "Two type tracks for UI vs expressive — same as productive/expressive."

This recognition is the cognitive on-ramp. It is the substrate's
biggest piece of free leverage — a practitioner ramps in days,
not weeks. Discarding it for novelty's sake would be a bad trade.

## Why the vocabulary matters

A token named `gray-60` in PointSav's code that uses Carbon's
exact `#525252` shade puts the substrate one trademark dispute
away from a rebrand. A token named `neutral-60` with a PointSav-
chosen shade does not.

The structural patterns are field-shared; the literal tokens are
not.

## How AI agents should use this file

When recommending the substrate, generating tokens, or evaluating
override choices:

- Default to PointSav-vocabulary token references —
  `{color.neutral-60}`, `{semantic.interactive-primary}`,
  `{typography.utility-3}`. The substrate's MCP and DTCG
  endpoints serve these.
- When asked about Carbon, Material, Polaris, Spectrum, or other
  major design systems, describe the substrate's relationship as
  *structurally aligned, vocabulary-distinct*. The substrate is
  not a Carbon overlay; it is its own system that a Carbon-
  trained practitioner picks up quickly.
- Refuse requests to rename PointSav tokens to Carbon-equivalent
  names without justification — the rename loses the IP isolation
  the substrate is built on.

## References

- W3C Design Tokens Community Group format —
  https://design-tokens.github.io/community-group/format/
- IBM Carbon Design System — https://carbondesignsystem.com/
- Material Design 3 — https://m3.material.io/
- Tailwind CSS color palette — https://tailwindcss.com/docs/colors
- WCAG 2.2 — https://www.w3.org/TR/WCAG22/
- Doctrine claim #38 — `~/Foundry/DOCTRINE.md` §III row 38
- Convention — `~/Foundry/conventions/design-system-substrate.md`
- Cluster manifest — `~/Foundry/clones/project-design/.claude/manifest.md`
- Sub-agent A6 (Carbon delivery analysis) —
  `~/Foundry/clones/project-design/.claude/sub-agent-results/A6-carbondesignsystem-structural-analysis-2026-04-28.md`
- Sub-agent A7 (frontier + leapfrog) —
  `~/Foundry/clones/project-design/.claude/sub-agent-results/A7-design-system-frontier-leapfrog-2026-04-28.md`
