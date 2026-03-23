<div align="center">

# PointSav Design System
### *Brutalismo Institucional y Física Óptica*

[ **System Monorepo** ](https://github.com/pointsav/pointsav-monorepo) | [ **Documentation Wiki** ](https://github.com/pointsav/content-wiki-documentation) | [ **Main Profile** ](https://github.com/pointsav)

*Despliegue Operativo:* [ **Woodfine Management Corp.** ](https://github.com/woodfine)

[ 🇬🇧 Read this document in English ](./README.md)

</div>

---

> [!WARNING]
> **MANDATO DE INFRAESTRUCTURA AGNÓSTICA**
> Este repositorio define la física universal y los alias semánticos. **Contiene cero colores de marca propietarios.** Los temas del cliente deben inyectarse en tiempo de ejecución a través de repositorios independientes de Activos de Medios.

### I. LA FILOSOFÍA DE LA ESTRATIFICACIÓN DE TOKENS
Para lograr una verdadera escalabilidad empresarial, un sistema de diseño debe separar la **realidad física** de la **intención semántica**. Si un desarrollador codifica un color hexadecimal específico (`#164679`) en un componente de botón, la infraestructura se vuelve frágil e imposible de tematizar.

Resolvemos esto utilizando una estricta Arquitectura de Tokens de Dos Niveles, construida para el estándar Leapfrog 2030 y limitada por nuestro mandato de Brutalismo Institucional:

1. **Tokens Globales (`tokens/global/`):** Realidades matemáticas sin opinión. Definen una cuadrícula de píxeles específica, pila de fuentes o sombra de profundidad.
2. **Alias Semánticos (`tokens/semantic/`):** Ranuras contextuales asignadas a componentes de la interfaz de usuario (ej., `color-action-primary`). 

Al forzar al HTML/CSS a consumir exclusivamente Alias Semánticos, permitimos al Cliente (Woodfine) o al Proveedor (PointSav) inyectar dinámicamente sus Tokens Globales propietarios en las ranuras de Alias vacías en el momento de la compilación.

### II. TOPOGRAFÍA DEL SISTEMA E ÍNDICE MAESTRO

#### 📐 `tokens/global/` (Física Óptica)
*Propiedades físicas en bruto y valores matemáticos absolutos.*
* **`token-global-assets.yaml`**: Rutas SVG sin procesar (GitHub, WhatsApp) abstraídas de cargas HTML.
* **`token-global-color.yaml`**: La paleta estructural maestra. Colores base y tonos algorítmicos.
* **`token-global-elevation.yaml`**: Arquitectura Z-Index y sombras paralelas dimensionales.
* **`token-global-print.yaml`**: Tamaños de punto exactos y física para la salida de PDF regulatorio.
* **`token-global-spacing.yaml`**: La cuadrícula base suiza de 8px y los puntos de interrupción de diseño.
* **`token-global-typography.yaml`**: Restricción de escala fluida, espaciado (tracking) y familias de fuentes principales.

#### 🧩 `tokens/semantic/` (Intención y Creación de Alias)
*Ranuras semánticas que puentean valores físicos a aplicaciones de componentes.*
* **`token-alias-telemetry.yaml`**: Define el diodo de transmisión y el contrato de carga JSON.
* **`token-alias-ui.yaml`**: Mapeo semántico para estados interactivos, fondos, jerarquías de texto y bordes estructurales.

#### ⚖️ `tokens/linguistic/` (La Ley)
*Reglas de escritura del Brutalismo Institucional y protocolos corporativos.*
* **`protocol-comm.yaml`**: Lógica de envío interno y mensajería externa.
* **`protocol-legal.yaml`**: Traducción de afirmaciones de mercado en hechos estructurales y defendibles.
* **`protocol-text.yaml`**: Reglas de escritura básicas del Brutalismo Institucional (ISO 24495-1).
* **`ps-protocol-telemetry-web.yaml`**: Infraestructura Digital y Postura de Privacidad.
* **`ps-protocol-trademark-web.yaml`**: Marca Comercial de PointSav y Defendibilidad de Derechos de Autor.

#### 🏛️ `architecture-decisions/` (ADRs)
*Registros históricos e inmutables de por qué el sistema está diseñado de esta manera.*
* **`DS-ADR-01` a `DS-ADR-04`**: Decisiones centrales que rigen la criptografía, la transparencia de la huella y la integración con GitHub.

---
*© 2026 PointSav Digital Systems™*
