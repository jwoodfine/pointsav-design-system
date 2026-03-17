<div align="center">

# PointSav Design System
### *Linguistic Protocols & Optical Physics*

**[ ⚙️ System Monorepo ](https://github.com/pointsav/pointsav-monorepo)** | **[ 📚 System Architecture Wiki ](https://github.com/pointsav/content-wiki-documentation)** | **[ 🏢 Main Profile ](https://github.com/pointsav)**

</div>

---

> [!WARNING]
> **AGNOSTIC INFRASTRUCTURE MANDATE**
> This repository defines universal physics and semantic aliases. **It contains zero proprietary brand colors.** Customer themes must be injected at runtime via independent Media Asset repositories.

## I. THE PHILOSOPHY OF TOKEN TIERING
To achieve true enterprise scalability, a design system must divorce **physical reality** from **semantic intent**. If a developer hardcodes a specific hex color (`#164679`) into a button component, the infrastructure becomes brittle and impossible to theme.

We solve this using a strict Two-Tier Token Architecture:

1. **Global Tokens (`token-global-*`):** Unopinionated mathematical realities. They define a specific pixel grid, font stack, or depth shadow.
2. **Alias Tokens (`token-alias-*`):** Semantic slots assigned to UI components (e.g., `color-action-primary`). 

By forcing the HTML/CSS to exclusively consume Alias Tokens, we allow the Customer (Woodfine) or the Vendor (PointSav) to dynamically inject their proprietary Global Tokens into the empty Alias slots at compile time.

## II. MASTER INDEX: OPTICAL PHYSICS & ASSETS
*Flat-file architectural definitions governing layout and rendering.*

| File | Subsystem | Description |
| :--- | :--- | :--- |
| `token-global-spacing.yaml` | Physics | The 8px Swiss Baseline Grid and layout breakpoints. |
| `token-global-typography.yaml` | Physics | Fluid scale clamping & core font families. |
| `token-global-elevation.yaml` | Physics | Z-Index architecture and dimensional shadows. |
| `token-global-print.yaml` | Physics | Exact point-sizes for regulatory PDF egress. |
| `token-global-assets.yaml` | Assets | Raw SVG paths (GitHub, WhatsApp) abstracted from HTML. |
| `token-alias-ui.yaml` | Aliases | Semantic mapping for colors, touch-targets, borders, and SVGs. |

## III. MASTER INDEX: SYSTEM CONFIGURATIONS
*Flat-file definitions for API routing and machine-readable data structures.*

| File | Subsystem | Description |
| :--- | :--- | :--- |
| `token-alias-telemetry.yaml` | System | Defines the transmission diode and JSON payload contract. |

## IV. MASTER INDEX: LINGUISTIC PROTOCOLS
*Nested strictly in `tokens/linguistic/` to enforce the Institutional Brutalism Mandate.*

| File | Subsystem | Description |
| :--- | :--- | :--- |
| `protocol-comm.yaml` | Syntax | Internal dispatch & asset distinction. |
| `protocol-legal.yaml` | Governance | Translation of market claims to structural facts. |
| `protocol-text.yaml` | Syntax | Institutional Brutalism core writing rules. |

---
*© 2026 PointSav Digital Systems™.*
