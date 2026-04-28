# When to use Select

Use a select for single-choice picking from a known, finite list
of 3–15 options. The native `<select>` element is the substrate's
canonical pattern — keyboard navigation (arrows, Home/End,
type-ahead) and screen-reader announcement work without
JavaScript.

## When to use

- Country picker, language picker, status picker, role picker.
- Any single-choice form field with a knowable enum.

## When not to use

- Two or three options visible at once: use radio buttons.
- 15+ options or open-ended search: use a combobox (subsequent
  milestone).
- Multiple selection: use a multi-select pattern (subsequent
  milestone).

## Native > custom

Custom `<div role="listbox">` selects are an anti-pattern under
WCAG 2.2 — replicating the native keyboard, focus, and announcement
behaviour correctly is more work than it appears, and most attempts
ship subtle bugs. The native `<select>` is the right answer at this
scale.
