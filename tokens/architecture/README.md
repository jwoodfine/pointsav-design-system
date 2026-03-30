# PointSav Design System: Institutional Architecture (DS-ADR-08)

**Classification:** System Logic & Engineering ("The Law")
**Objective:** Provide strict geometric, typographic, and routing tokens for rapid assembly of institutional flowcharts and corporate architectures.

## The Assembly Line Workflow

This directory contains the visual building blocks for the Leapfrog 2030 standard. **Do not store content or data here.** This repository is strictly for rendering the framework.

### The Core Tokens
1. **`ds-adr-08-core.css` (The Law)**
   - The single source of truth for all print dimensions (1056x816), institutional typography, node geometry, and routing vector colors. 
   - *Rule of Engagement:* Never write inline CSS in an architecture file. If a color or stroke needs updating, update it here.

2. **`ds-adr-08-canvas.html` (The Boilerplate)**
   - The blank slate. It contains the locked `print-canvas` wrapper, the DS-ADR-08 title injection zones, and the legal disclaimer anchors.
   - *Rule of Engagement:* Always start a new architecture by duplicating this file.

3. **`ds-adr-08-component-library.html` (The Nodes)**
   - A copy-paste repository of raw HTML snippets for every approved entity shape (Standard Green, Yellow Ellipse, Tall Blue, etc.).
   - *Rule of Engagement:* Copy the required block, paste it into your active canvas, and adjust the `left` and `top` inline styles to position it.

4. **`ds-adr-08-routing-api.html` (The Vectors)**
   - The centralized SVG definitions for all institutional routing lines and arrowheads.
   - *Rule of Engagement:* Inject the base `<svg>` block directly under the title container in your canvas. Add `<path>` elements using the predefined CSS classes (e.g., `.route-solid-green`) to map relationships.

## Execution Sequence
1. Receive completed `WCP-ARCHITECTURE-MANIFEST.txt` from Woodfine operations.
2. Duplicate `ds-adr-08-canvas.html`.
3. Copy/Position required nodes from the component library.
4. Draw vector relationships using the routing API.
5. Inject the text payloads from the manifest.
