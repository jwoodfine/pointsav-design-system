---
schema: foundry-guide-v1
title: Guide — Badge
component: badge
category: deployment
---

# Deployment Guide

## Overview
A small, inline status indicator. Carries a short label and a tone.

## Technical Recipe

### HTML
```html
<span class="ps-badge ps-badge--{{variant}}">{{label}}</span>
```

### CSS
```css
.ps-badge{display:inline-flex;align-items:center;padding:0 var(--ps-space-3,8px);min-height:1.25rem;border-radius:var(--ps-corner-1,2px);font-size:.75rem;font-weight:600;line-height:1.34;letter-spacing:.16px}.ps-badge--neutral{background-color:var(--ps-surface-subtle,#f5f6f8);color:var(--ps-ink-secondary,#4a4f59)}.ps-badge--primary{background-color:var(--ps-support-info-bg,#eef3ff);color:var(--ps-support-info,#234ed8)}.ps-badge--positive{background-color:var(--ps-support-positive-bg,#e8f6ed);color:var(--ps-support-positive,#16602b)}.ps-badge--caution{background-color:var(--ps-support-caution-bg,#fff5e1);color:var(--ps-support-caution,#7a520a)}.ps-badge--critical{background-color:var(--ps-support-critical-bg,#fceaea);color:var(--ps-support-critical,#7d1414)}
```

## Accessibility
Badge is decorative status; the surrounding context provides meaning. If the badge IS the only signal of state, wrap with a screen-reader-friendly element: <span class='sr-only'>Status: </span><span class='ps-badge'>active</span>.
