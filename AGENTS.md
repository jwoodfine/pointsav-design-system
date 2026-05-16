# AGENTS.md

> Vendor-neutral pointer file for coding agents (per the AGENTS.md
> spec, donated to the Linux Foundation December 2025).
>
> This repo's substantive operational guide for AI agents lives
> in **`CLAUDE.md`** at this same directory.

## Quick reference

- **Operational guide**: `CLAUDE.md` (this directory)
- **Open work queue**: `NEXT.md` (this directory)
- **Constitutional charter**: `~/Foundry/DOCTRINE.md`
- **Workspace navigation**: `~/Foundry/CLAUDE.md`

## This repo

`pointsav-design-system` is the canonical DTCG token source and component recipe
library for the PointSav design system substrate (Doctrine claim #38). It supplies:

- `tokens/dtcg-bundle.json` — the master DTCG token bundle (generic + brand layers)
- `components/<name>/guide.md` — component usage guides (HTML, CSS, ARIA)
- `docs/foundations/` — conceptual foundation documentation (color, typography, spacing, motion)
- `docs/accessibility/` — cross-cutting accessibility specifications
- `dtcg-vault/research/` — AI-readable design decision research backplane

Content published at `design.pointsav.com`. Other project-* archives consume tokens
from this repo; they send new DESIGN-TOKEN-CHANGE and DESIGN-COMPONENT drafts back
to project-design for integration here.

## License

Apache 2.0. Trademarks reserved per `TRADEMARK.md`.

---

*Per `~/Foundry/conventions/root-files-discipline.md` Tier 2.*
