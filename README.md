<div align="center">

# PointSav Design System
### *Institutional Brutalism & Optical Physics*

**[ ⚙️ System Monorepo ](https://github.com/pointsav/pointsav-monorepo)** | **[ 📚 System Architecture Wiki ](https://github.com/pointsav/content-wiki-documentation)** | **[ 🏢 Main Profile ](https://github.com/pointsav)**

</div>

---

> [!WARNING]
> **AGNOSTIC INFRASTRUCTURE MANDATE**
> This repository defines universal physics and semantic aliases. **It contains zero proprietary brand colors.** Customer themes must be injected at runtime via independent Media Asset repositories.

## I. THE PHILOSOPHY OF TOKEN TIERING
To achieve true enterprise scalability, a design system must divorce **physical reality** from **semantic intent**. If a developer hardcodes a specific hex color (\`#164679\`) into a button component, the infrastructure becomes brittle and impossible to theme.

We solve this using a strict Two-Tier Token Architecture, built for the Leapfrog 2030 standard and constrained by our Institutional Brutalism mandate:

1. **Global Tokens (\`tokens/global/\`):** Unopinionated mathematical realities. They define a specific pixel grid, font stack, or depth shadow.
2. **Semantic Aliases (\`tokens/semantic/\`):** Contextual slots assigned to UI components (e.g., \`color-action-primary\`). 

By forcing the HTML/CSS to exclusively consume Semantic Aliases, we allow the Customer (Woodfine) or the Vendor (PointSav) to dynamically inject their proprietary Global Tokens into the empty Alias slots at compile time.

## II. SYSTEM TOPOGRAPHY & MASTER INDEX

### 📐 \`tokens/global/\` (Optical Physics)
*Raw physical properties and absolute mathematical values.*
* **\`token-global-assets.yaml\`**: Raw SVG paths (GitHub, WhatsApp) abstracted from HTML payloads.
* **\`token-global-color.yaml\`**: The master structural palette. Base colors and algorithmic shades.
* **\`token-global-elevation.yaml\`**: Z-Index architecture and dimensional drop-shadows.
* **\`token-global-print.yaml\`**: Exact point-sizes and physics for regulatory PDF egress.
* **\`token-global-spacing.yaml\`**: The 8px Swiss Baseline Grid and layout breakpoints.
* **\`token-global-typography.yaml\`**: Fluid scale clamping, tracking, and core font families.

### 🧩 \`tokens/semantic/\` (Intent & Aliasing)
*Semantic slots that bridge physical values to component applications.*
* **\`token-alias-telemetry.yaml\`**: Defines the transmission diode and JSON payload contract.
* **\`token-alias-ui.yaml\`**: Semantic mapping for interactive states, backgrounds, text hierarchies, and structural borders.

### ⚖️ \`tokens/linguistic/\` (The Law)
*Institutional Brutalism writing rules and corporate protocols.*
* **\`protocol-comm.yaml\`**: Internal dispatch & external messaging logic.
* **\`protocol-legal.yaml\`**: Translation of market claims into structural, defensible facts.
* **\`protocol-text.yaml\`**: Institutional Brutalism core writing rules (ISO 24495-1).
* **\`ps-protocol-telemetry-web.yaml\`**: Digital Infrastructure & Privacy Posture.
* **\`ps-protocol-trademark-web.yaml\`**: PointSav Trademark & Copyright Defensibility.

### 🏛️ \`architecture-decisions/\` (ADRs)
*Historical, immutable logs of why the system is designed this way.*
* **\`DS-ADR-01\` to \`DS-ADR-04\`**: Core decisions governing cryptography, footprint transparency, and GitHub integration.

---
*© 2026 PointSav Digital Systems™.*
