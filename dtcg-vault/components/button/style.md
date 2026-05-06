# Button — Style

Token references resolve from the active theme. The component
never hardcodes a colour, font, spacing, or motion value.

## Color

### Primary variant

| State | Background | Text |
|---|---|---|
| Default | `{semantic.interactive-primary}` | `{semantic.ink-on-interactive}` |
| Hover | `{semantic.interactive-primary-hover}` | `{semantic.ink-on-interactive}` |
| Pressed | `{semantic.interactive-primary-pressed}` | `{semantic.ink-on-interactive}` |
| Disabled | `{semantic.interactive-primary-disabled}` | `{semantic.ink-disabled}` |
| Focus ring | `{semantic.focus-ring}` | — |

### Secondary variant

| State | Background | Text |
|---|---|---|
| Default | `{semantic.interactive-secondary}` | `{semantic.ink-on-interactive}` |
| Hover | `{semantic.interactive-secondary-hover}` | `{semantic.ink-on-interactive}` |
| Pressed | `{semantic.interactive-secondary-pressed}` | `{semantic.ink-on-interactive}` |

### Ghost variant

| State | Background | Text |
|---|---|---|
| Default | `transparent` | `{semantic.ink-primary}` |
| Hover | `{semantic.interactive-ghost-hover}` | `{semantic.ink-primary}` |
| Pressed | `{semantic.interactive-ghost-pressed}` | `{semantic.ink-primary}` |

### Critical variant

| State | Background | Text |
|---|---|---|
| Default | `{semantic.interactive-critical}` | `{semantic.ink-on-critical}` |
| Hover | `{semantic.interactive-critical-hover}` | `{semantic.ink-on-critical}` |
| Pressed | `{semantic.interactive-critical-pressed}` | `{semantic.ink-on-critical}` |

## Typography

| Element | Token |
|---|---|
| Label | `{typography.utility-4}` (16/24, weight 600) |

## Structure

| Property | Token |
|---|---|
| Min height | 2.5rem (40px) |
| Horizontal padding | `{size.space-5}` (16px) |
| Icon-label gap | `{size.space-3}` (8px) |
| Border radius | `{border.corner-2}` (4px) |
| Focus ring width | `{border.stroke-2}` (2px) |
| Focus ring offset | 2px |

## Motion

| Property | Duration | Curve |
|---|---|---|
| Background colour transition (hover/pressed) | `{duration.speed-2}` (120ms) | `{motion.ease-utility}` |

## Anatomy diagram

Future: interactive SVG anatomy diagram. v0.0.2 ships the structure
table; contributors with SVG/Figma access can author the diagram.
