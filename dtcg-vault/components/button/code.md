# Button — Code

The substrate's component recipes are framework-agnostic
HTML+CSS+ARIA bundles. Every framework consumes the same source.

## Get the recipe

### Via shadcn-compatible CLI

The substrate exposes a [shadcn-registry-compatible
endpoint](/r/registry.json) at `https://design.pointsav.com/r/`.
AI codegen tools — v0, Cursor, Claude Code, Windsurf — and the
shadcn CLI use the same endpoint:

```bash
npx shadcn add https://design.pointsav.com/r/button.json
```

This installs the button recipe into `<your-project>/components/ui/button.*`.

### Via Model Context Protocol

The substrate's MCP server (at `https://design.pointsav.com/mcp`)
exposes:

```json
{
  "method": "get_component_recipe",
  "params": { "name": "button", "theme": "pointsav-brand" }
}
```

AI agents query this at decode time; the response is a complete
recipe (HTML, CSS, ARIA, tokens consumed) plus the resolved
token values for the requested theme.

### Via direct HTTP

Machine-readable JSON:

```bash
curl https://design.pointsav.com/api/components/button.json
```

DTCG-format token subset:

```bash
curl -H "Accept: application/design-tokens+json" \
  https://design.pointsav.com/api/tokens/component/button.dtcg.json
```

### Via Git

Customers running their own substrate fork the
`dtcg-vault/components/button/` directory in the
[`pointsav-design-system`](https://github.com/pointsav/pointsav-design-system)
Git repository.

## HTML + CSS recipe

```html
<button type="button" class="ps-btn ps-btn--primary">
  <span class="ps-btn__label">Save changes</span>
</button>
```

```css
.ps-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--ps-space-3, 8px);
  min-height: 2.5rem;
  padding: 0 var(--ps-space-5, 16px);
  border: 0;
  border-radius: var(--ps-corner-2, 4px);
  font-family: inherit;
  font-size: 0.875rem;
  font-weight: 600;
  line-height: 1.43;
  cursor: pointer;
  transition: background-color
              var(--ps-speed-2, 120ms)
              var(--ps-ease-utility, cubic-bezier(.2,0,.4,1));
  white-space: nowrap;
}

.ps-btn:focus-visible {
  outline: 2px solid var(--ps-focus-ring, #234ed8);
  outline-offset: 2px;
}

.ps-btn--primary {
  background-color: var(--ps-interactive-primary, #234ed8);
  color: var(--ps-ink-on-interactive, #fff);
}

.ps-btn--primary:hover {
  background-color: var(--ps-interactive-primary-hover, #173ab1);
}
```

The full recipe (all four variants) is at the registry endpoint
above.

## React adapter (community)

```jsx
function Button({ variant = 'primary', children, ...props }) {
  return (
    <button
      type="button"
      className={`ps-btn ps-btn--${variant}`}
      {...props}
    >
      <span className="ps-btn__label">{children}</span>
    </button>
  );
}
```

## Vue adapter (community)

```vue
<template>
  <button type="button" :class="['ps-btn', `ps-btn--${variant}`]">
    <span class="ps-btn__label"><slot /></span>
  </button>
</template>

<script setup>
defineProps({ variant: { type: String, default: 'primary' } });
</script>
```

## Other framework adapters

The substrate's recipe model is framework-agnostic. Adapters for
Svelte, SolidJS, Angular, Web Components, Astro, and server-
rendered (Rust/Go/PHP/Python) targets are contributor work.
The recipe is the source; the adapter is the consumption path.
