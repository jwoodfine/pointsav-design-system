<div align="center">

<img src="https://raw.githubusercontent.com/pointsav/pointsav-media-assets/main/ASSET-SIGNET-MASTER.svg" width="72" alt="PointSav Design System">

# Sistema de Diseño PointSav
### Protocolos Lingüísticos y Estándares Visuales
*La fuente única de verdad para la voz institucional y la identidad visual en cada despliegue de PointSav.*

[![WCAG: 2.2 AAA](https://img.shields.io/badge/WCAG-2.2_AAA-0075ca.svg?style=flat-square)](#estándares-visuales)
[![Licencia: Propietaria](https://img.shields.io/badge/Licencia-Propietaria-e36209.svg?style=flat-square)](#uso-y-licenciamiento)

<br/>

**[→ Monorepo de Ingeniería](https://github.com/pointsav/pointsav-monorepo)** &nbsp;·&nbsp; **[→ Wiki de Documentación](https://github.com/pointsav/content-wiki-documentation)** &nbsp;·&nbsp; **[→ pointsav.com](https://pointsav.com)**

</div>

---

## Qué es Este Repositorio

La mayoría de los sistemas de diseño son colecciones de colores y tipografías. Este es diferente.

PointSav opera una plataforma donde los mismos datos subyacentes deben proyectarse con precisión en divulgaciones públicas para inversores, terminales internas de operadores, presentaciones regulatorias y superficies de marketing bilingüe. Un color que se muestra correctamente en modo oscuro debe mantener su validez legal en una presentación regulatoria impresa. Un protocolo lingüístico que enruta datos estructurados de forma determinista debe aplicarse de manera consistente tanto en Vancouver como en Madrid.

El sistema de diseño aplica estas restricciones como tokens legibles por máquina — archivos YAML que son consumidos automáticamente por cada superficie de despliegue.

---

## Protocolos Lingüísticos

El lenguaje en un contexto institucional no es una preferencia estilística. Es un compromiso estructural. La palabra incorrecta en una divulgación para inversores es un evento regulatorio.

| Archivo de Token | Qué gobierna |
|:---|:---|
| `protocol-text.yaml` | Reglas de escritura fundamentales — tono, registro, estructura de oraciones, vocabulario prohibido |
| `protocol-comm.yaml` | Despacho interno — distinción de activos, clasificación de enrutamiento |
| `protocol-extract.yaml` | Reglas de análisis determinista — cero inferencia de IA, gramática léxica estricta |
| `protocol-legal.yaml` | Traducción de afirmaciones de mercado a hechos estructurales — estándares de lenguaje regulatorio |
| `protocol-memo.yaml` | Síntesis del libro mayor ejecutivo — estructura de memorandos, cadena de autoridad |
| `protocol-translate.yaml` | Reglas de límite bilingüe — bloqueos de nombres propios, manejo de términos específicos por jurisdicción |

`protocol-translate.yaml` merece una mención especial. PointSav opera en Canadá, Estados Unidos, España y México. El mismo concepto de inversión — una Solución de Tenencia Directa — tiene una designación legal diferente en cada jurisdicción. El archivo de protocolo codifica qué términos son traducibles y cuáles deben permanecer en su idioma original independientemente del idioma del documento. Esto previene la fractura legal en documentos bilingües.

---

## Estándares Visuales

| Archivo de Token | Qué gobierna |
|:---|:---|
| `typography.yaml` | Composición tipográfica fluida, proporciones de cuadrícula suiza, reglas de renderizado de subpíxeles |
| `spacing.yaml` | Sistema de cuadrícula de 8px, mínimos de objetivo táctil, densidad accesible |
| `color.yaml` | Paleta específica por entidad, cumplimiento de modo oscuro, ratios de contraste |
| `TOKEN-UI-PHYSICS.yaml` | Definiciones estructurales WCAG 2.2 AAA — ratios de contraste, indicadores de foco, movimiento |
| `TOKEN-TYPOGRAPHY-RENDER.yaml` | Antialias de subpíxeles, consistencia de renderizado multiplataforma |

---

*© 2026 PointSav Digital Systems™. Todos los derechos reservados.*

*→ English version: [README.md](./README.md)*
