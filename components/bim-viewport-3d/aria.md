# bim-viewport-3d — accessibility

## Role and structure

- Container is `<section aria-label="3D viewport">`.
- 3D canvas is `<canvas aria-label="3D model canvas">` — canvas
  content is not directly inspectable by AT; selection state is
  surfaced via the status bar and the live `bim-properties-panel`.
- Toolbar is `<div role="toolbar" aria-label="Viewport controls">`
  with `<button>` children carrying `aria-label`.
- The NavCube is presentational (`aria-hidden="true"`); functionally
  duplicated by keyboard view-direction shortcuts (1–6 for
  ±X / ±Y / ±Z).

## Selection synchronisation

- Selecting an element in the canvas updates the live region in
  `bim-properties-panel` (host integration).
- Selection from `bim-spatial-tree` (key-actuated) flows to the
  viewport via host integration.

## Keyboard navigation

| Key | Action |
|---|---|
| 1 / 2 / 3 / 4 / 5 / 6 | View along ±X / ±Y / ±Z axes (NavCube equivalent) |
| F | Fit selected element / fit view if no selection |
| Arrow keys | Pan (with shift) or orbit |
| `+` / `-` | Zoom in / out |
| `S` | Toggle section plane |
| `B` | Capture BCF viewpoint (workplace mode only) |
| Tab | Move focus to toolbar |

## Mode-prop behaviour

- `data-mode="workplace"` — toolbar buttons enabled; xeokit-bim-viewer
  embeds at host-integration time; AGPL-3.0 distribution.
- `data-mode="console"` — toolbar buttons disabled; viewport
  optionally degrades to static SVG plan thumbnail to preserve
  EUPL-1.2 boundary; selection arrives from SpatialTree only
  (no canvas selection).

## Don't

- Don't pipe IFC bytes over IPC. xeokit canvas loads XKT files via
  `convertFileSrc()` + Tauri's `asset:` protocol; large model data
  never crosses the IPC boundary. (BB.3 finding.)
- Don't bundle xeokit's standalone CSS; let the runtime integration
  pull it via npm/CDN per host-framework decision.
