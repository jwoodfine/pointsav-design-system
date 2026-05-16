# docs/ — Design system content directory

Content files for `design.pointsav.com`. Section mapping:

| Subdirectory | Site section | Rule |
|---|---|---|
| `foundations/` | **Foundations** | Conceptual prose per foundation. NOT embedded in token entries. One EN + one ES file per foundation. |
| `wiki-surface/` | **App surfaces → PointSav Wiki** | Compositional overviews of the wiki product surface. NOT flattened into generic Components. |
| `accessibility/` | **Accessibility** | Cross-cutting WCAG + neurodiversity hub. Co-located with Accessibility section only; bidirectional links to/from Component pages mandatory. |

## Intake rules

- All files in `foundations/` require an `.es.md` pair.
- All files in `wiki-surface/` require an `.es.md` pair.
- All files in `accessibility/` require an `.es.md` pair.
- New subdirectories require an update to `../site-nav.yaml` before content is added.
- Component usage guides do NOT live here — they live at `../components/<name>/guide.md`.
- Research backplane files do NOT live here — they live at `../dtcg-vault/research/`.

## Section content rules

**Foundations:** explain the *why* of each design foundation and the three-layer model
(primitive → semantic → component). Do not list individual token values — the Tokens
section auto-generates from `dtcg-bundle.json`.

**wiki-surface:** describe how components compose into the wiki product surface.
Cross-link each component mentioned to its `../components/<name>/guide.md` page.

**accessibility:** document cross-cutting patterns that govern multiple components.
Each page must list the components it governs. Each Component page must link back here.
