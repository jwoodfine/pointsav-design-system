# bim-properties-panel — accessibility

## Role and structure

- Container is `<aside aria-label="Element properties">`.
- Each Pset / Qto group is a `<section>` with an `<h4>` heading.
- Each property is a `<dt>` / `<dd>` pair within a `<dl>`.
- The element subject (class + GUID) appears below the panel
  heading in a `<p class="bim-properties-panel__subject">`.

## Live region

- The selected element is announced when changed. The container has
  `aria-live="polite"` (added at host-framework integration time;
  not in the static recipe to avoid it triggering on every recipe
  render).

## Mode-prop behaviour

- `data-mode="workplace"` — `<dd>` is replaced by appropriate
  `<input>` / `<select>` controls at the framework integration layer.
  The recipe carries the static console view; the framework swaps
  on workplace.
- `data-mode="console"` — read-only `<dt>` / `<dd>` pairs.

## Keyboard navigation

| Key | Action |
|---|---|
| Tab / Shift-Tab | Move focus between editable fields (workplace mode only) |
| Enter | Commit edit (workplace) |
| Escape | Cancel edit and revert (workplace) |

## Don't

- Don't author custom Pset names without registering them in the
  IFC PsetSet template. Custom property sets must declare a custom
  Pset namespace.
- Don't display GlobalId without a copy-to-clipboard affordance —
  IFC GUIDs are 22 characters of base-64 and useful only when
  copyable.
