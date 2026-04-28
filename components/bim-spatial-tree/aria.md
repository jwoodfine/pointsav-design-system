# bim-spatial-tree — accessibility

## Role and structure

- Container is `<aside aria-label="Spatial hierarchy">`.
- Tree is `<ul role="tree">`.
- Each spatial item is `<li role="treeitem" aria-expanded="…">`.
- Children are `<ul role="group">`.
- The `aria-expanded` attribute reflects the collapse/expand state.
  Storey-level nodes default to `aria-expanded="true"`; their child
  `<ul role="group">` is `hidden` by default to defer per BB.4
  ("expanded-to-storey, no auto-expand to spaces").

## Selection

- Selected node carries `aria-selected="true"`.
- Multi-select is allowed in workplace mode (`Ctrl/Cmd-click`,
  `Shift-click`); console mode is single-select.

## Keyboard navigation

| Key | Action |
|---|---|
| Arrow Up / Down | Move focus between sibling tree items |
| Arrow Right | Expand the focused item if it has children; otherwise focus first child |
| Arrow Left | Collapse the focused item if expanded; otherwise focus parent |
| Enter / Space | Activate (select) the focused item |
| Home / End | Focus first / last visible tree item |
| `/` (slash) | Move focus to the search input |

## Search

- Search input is `<input type="search" aria-label="Search spaces">`.
- Search filters the tree by space name (`IfcSpace.LongName`,
  `IfcSpace.Name`), case-insensitive substring match.
- Match results expand the matching path automatically; non-matching
  branches collapse.

## Mode-prop behaviour

- `data-mode="workplace"` — affordance for drag-to-reorder and
  multi-select; cursor: `grab`.
- `data-mode="console"` — read-only; cursor: `pointer`; no
  drag-to-reorder; single-select only.

## Don't

- Don't auto-expand into the space level. Bonsai's storey-default
  expansion is the convention every AEC practitioner expects.
- Don't reuse a generic scene-graph viewer (the Outliner-as-Tree
  pattern). Build the dedicated SpatialTree widget.
