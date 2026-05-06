---
title: Badge — Accessibility
---

# Accessibility

Badges are used to highlight an item's status or for small amounts of information. They are purely visual indicators and must be accessible to screen readers.

## WCAG 2.2 Conformance

| Criteria | Status | Notes |
| :--- | :--- | :--- |
| **1.4.3 Contrast (Minimum)** | Pass | All badge background/text combinations meet 4.5:1 ratio. |
| **1.3.1 Info and Relationships** | Pass | Badges use semantic color coding. |

## ARIA Roles

Badges typically do not require specific ARIA roles unless they represent a status change that needs to be announced. In those cases, use `role="status"`.

- Use `aria-label` to provide context if the badge text is ambiguous (e.g., "3" in a badge might need `aria-label="3 notifications"`).
