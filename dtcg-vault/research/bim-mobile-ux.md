# BIM Mobile UX — Research Notes

**Source:** design-research-mobile-bim-ux.draft.md (project-bim, 2026-05-06)  
**Cites:** xeokit-sdk, tauri-2-10, ifc-4-3

---

## Layout Patterns for Small Viewports

**Sidebar drawer.** On viewports narrower than 768px, the navigation sidebar collapses into a
modal drawer triggered by a menu icon in the topbar. The drawer overlays content; it does not
push. Overlay is dismissed by tap-outside or swipe-left.

**Bottom sheet property panel.** The Properties Panel component renders as a bottom sheet on
mobile rather than a side panel. Two states:

- **Peek** (collapsed): shows element type, IFC class, and Uniclass reference. 64px height
  above viewport bottom.
- **Expanded**: full property set table, regulation summary row, climate zone summary row.
  Scrollable. Drag handle at top.

Swipe-up to expand, swipe-down to peek, second swipe-down to dismiss.

## 3D Viewport Touch Navigation

Touch gesture map for xeokit-sdk viewport:

| Gesture | Action |
|---|---|
| Single-finger drag | Orbit / rotate |
| Two-finger drag | Pan |
| Pinch | Zoom |
| Tap | Select element |
| Double-tap | Fit to selection |

**Tap-to-select feedback.** A brief highlight pulse (200ms, 0.3 opacity increase) confirms
element selection. This replaces hover-highlight, which is not available on touch.

**Occlusion ghosting.** When an element behind other geometry is selected (e.g., a structural
column behind a wall), the obscuring elements reduce to 15% opacity for 2 seconds, then
restore. This makes the selected element visible without a separate x-ray mode toggle.

## Performance Targets

| Metric | Target |
|---|---|
| Time to first 3D frame | ≤ 3s on mid-range Android (Samsung Galaxy A-series) |
| Touch response latency | ≤ 16ms (single frame at 60fps) |
| IFC geometry cache memory budget | ≤ 150MB (browser context) |

## Open Questions

1. xeokit-sdk touch event handling on iOS Safari requires a workaround for passive event
   listener warnings. The specific version of xeokit and the recommended `touchstart` handler
   approach is not yet confirmed for Tauri 2.x webview.
