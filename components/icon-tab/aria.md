---
schema: foundry-doc-v1
type: aria-spec
component: icon-tab
state: authoritative
audience: vendor-public
---

# ARIA Specification — icon-tab

## Element semantics

The icon-tab component is a native `<a>` element. No ARIA role override is needed —
`<a href>` carries the implicit link role. Do not use `role="button"` (this is navigation,
not an action).

## Required attributes

| Attribute | Where | Value |
|---|---|---|
| `aria-label` | `<a>` | `"<Destination name> (opens in new tab)"` |
| `aria-hidden="true"` | inline SVG | Prevents icon path from being announced |
| `focusable="false"` | inline SVG | Required in older SVG agents |
| `rel="noopener"` | `<a>` | Required alongside `target="_blank"` |

## aria-label pattern

The aria-label MUST:
1. Name the destination clearly — e.g., "Fleet Manifest", "Design Files", not just "GitHub"
2. Include "(opens in new tab)" suffix — WCAG 2.4.4 Link Purpose, Level AA
3. Be written in title case (Woodfine brand voice)

Example: `aria-label="Fleet Manifest (opens in new tab)"`

Do NOT: `aria-label="GitHub"` — fails to describe the destination.

## Focus behaviour

The component receives standard browser focus. `focus-visible` outline is provided in
recipe.css via `:focus-visible` pseudo-class. No JavaScript focus management needed.

## Screen reader announcement

With the above attributes, screen readers announce:
> "Fleet Manifest (opens in new tab), link"

The icon SVG is suppressed via `aria-hidden="true"`. The label span provides the
visible + accessible text.

---

## Open questions (pending project-design decision)

### 1. Inline SVG vs CSS background-image icon slot

**Current:** inline SVG with `fill="currentColor"` — icon inherits text colour automatically;
no separate icon colour token needed.

**Alternative:** CSS `background-image` on `::before` pseudo-element — removes the HTML
dependency on icon content (designer swaps the modifier class only) but loses colour
inheritance (`background-image` cannot use `currentColor`; requires a separate
`--icon-color` token or filter workaround).

**Recommendation (project-design to confirm):** keep inline SVG for this release.
The currentColor inheritance is clean; the modifier-class pattern (`wf-icon-tab--github`)
achieves the same slot-swap goal via class switching.

### 2. Ghost variant

**Current:** `template-agnostic-ui.html` uses a bordered, light-background `.btn` variant
of the GitHub icon button alongside the filled version.

**Option A:** Register as `wf-icon-tab--ghost` modifier — same component, different fill.
**Option B:** Treat as a separate `icon-btn` component — different semantic emphasis
(secondary / inline action vs primary egress tab).

**Recommendation (project-design to confirm):** defer to next milestone; commit the filled
primary variant now.

### 3. --ps-font-display token

The component uses `var(--ps-font-display)` for the Oswald/Barlow Condensed display
typeface. This token is not yet in `tokens/dtcg-bundle.json` — currently resolved via
the Woodfine theme's `var(--display)` custom property. A DESIGN-TOKEN-CHANGE is needed
to formalise `--ps-font-display` before the component is used outside the Woodfine theme.
