# When to use Surface

Use a surface to group related content visually without imposing
a layout. Three elevation variants give one canonical answer per
hierarchy level.

| Variant | When to use |
|---|---|
| **Subtle** | Background sections — sidebars, side panels, secondary content regions |
| **Base** | In-flow cards — record summaries, list items with structure |
| **Elevated** | Above-page layers — modals, dropdowns, popovers, toasts |

## Composition

Surface is a primitive — author your own card, panel, dialog by
composing the surface variant with appropriate inner spacing,
typography, and structure. The substrate does not ship a
`Card` component because every "card" pattern in production is
slightly different; the Surface primitive plus prose-rendering
discipline is more durable than 47 specific card variants.
