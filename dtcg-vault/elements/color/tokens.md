# Color — Tokens

The full DTCG bundle for the active theme is at
[`/tokens.json`](/tokens.json) and
[`/api/tokens/<theme>.dtcg.json`](/api/tokens/pointsav-brand.dtcg.json)
(with `Content-Type: application/design-tokens+json`).

## Primitives — Neutral

| Token | Value | Use for |
|---|---|---|
| `color.white` | `#ffffff` | Pure white reference |
| `color.neutral-10` | `#f5f6f8` | Page-background subtle |
| `color.neutral-20` | `#e6e8ec` | Border-subtle |
| `color.neutral-30` | `#cdd1d8` | Subtle dividers |
| `color.neutral-40` | `#aab0bb` | Border-strong |
| `color.neutral-50` | `#878d99` | Disabled / placeholder ink |
| `color.neutral-60` | `#666c78` | Tertiary text |
| `color.neutral-70` | `#4a4f59` | Secondary text |
| `color.neutral-80` | `#33373e` | Inverse surface base |
| `color.neutral-90` | `#1f2125` | Heavy inverse surface |
| `color.neutral-100` | `#0e0f12` | Primary text (ink-primary) |
| `color.black` | `#000000` | Pure black reference |

## Primitives — Primary

| Token | Value |
|---|---|
| `color.primary-10` | `#eef3ff` |
| `color.primary-20` | `#d3deff` |
| `color.primary-30` | `#a6bcff` |
| `color.primary-40` | `#7392ff` |
| `color.primary-50` | `#3f6cf2` |
| `color.primary-60` | `#234ed8` |
| `color.primary-70` | `#173ab1` |
| `color.primary-80` | `#0c2785` |
| `color.primary-90` | `#04165a` |

`primary-60` is the canonical PointSav-brand interactive color.

## Primitives — Support families

Positive, Caution, Critical — each ships 10/30/50/60/70 steps.

| Family | 10 (background) | 60 (text) |
|---|---|---|
| Positive | `#e8f6ed` | `#26823f` |
| Caution | `#fff5e1` | `#a87514` |
| Critical | `#fceaea` | `#a52323` |

For the full bundle including all steps and semantic-layer
overrides, see the live DTCG export.
