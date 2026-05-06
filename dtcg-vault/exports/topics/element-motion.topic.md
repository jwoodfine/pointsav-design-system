---
schema: foundry-topic-v1
title: Foundation — motion
origin: https://design.pointsav.com/elements/motion/overview/
doctrine_alignment: 38
---

# Motion

Motion communicates causation. The substrate ships four easing
curves and six duration steps. Combine them per interaction
class.

## Easing curves

| Token | Curve | Use for |
|---|---|---|
| `motion.ease-utility` | `cubic-bezier(.2, 0, .4, 1)` | Productive interactions — buttons, inputs, tabs |
| `motion.ease-display` | `cubic-bezier(.4, .14, .3, 1)` | Expressive interactions — toasts, modals, hero |
| `motion.ease-enter` | `cubic-bezier(0, 0, .4, 1)` | Element appearing |
| `motion.ease-exit` | `cubic-bezier(.2, 0, 1, 1)` | Element disappearing |

Productive curves are designed for short durations (≤200ms);
expressive curves work at longer durations (≥320ms) where the
extra weight is perceptible.

## Duration steps

| Token | Value | Use for |
|---|---|---|
| `duration.speed-1` | 70ms | Imperceptible — color hover |
| `duration.speed-2` | 120ms | Quick — button press, focus ring |
| `duration.speed-3` | 200ms | Snappy — tab switch |
| `duration.speed-4` | 320ms | Smooth — toast appearance, drawer slide |
| `duration.speed-5` | 480ms | Considered — modal entrance |
| `duration.speed-6` | 720ms | Deliberate — hero animation |

## Reduced motion

`prefers-reduced-motion: reduce` is honoured at all interaction
layers. Component recipes ship with the media-query override
included; consumers inherit. Do not bypass the override —
motion-sensitive users have explicitly opted out.

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

## Anti-patterns

- Animations that block user input (modals fading in for 700ms
  while the focus is unfocusable). Modal entrance is `speed-5`
  for the visual; focus moves immediately at duration 0.
- Decorative motion that adds time to a productive task. Save
  expressive motion for moments that warrant the user's attention.
- Off-scale durations (350ms, 500ms). The 6-step scale covers
  every interaction class.
