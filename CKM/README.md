---
title: "CKM UMBRAL — Guía de uso, naming y memoria del proyecto"
area: producto
audiencia: interno
tipo: politica
sensibilidad: interno
owner: "@santiromero1"
estado: vigente
revision-cada: "90d"
ultima-revision: "2026-06-08"
tags: [ckm, guia, naming, frontmatter, memoria, proceso, spec]
relacionado:
  - marca/MARCA_UMBRAL.md
  - producto/UMBRAL_PRODUCTO.md
---

# CKM UMBRAL — Guía y memoria del proyecto

**CKM = Centralized Knowledge Management.** Esta carpeta es la fuente de verdad de UMBRAL: marca, producto, diseño, software y negocio. Todo lo que necesite saber una persona —o un agente de AI— para entender o construir UMBRAL vive acá, en `.md` versionados.

Este documento cumple dos funciones:

1. **Guía de uso** — cómo está ordenado el CKM, cómo se nombran los archivos, qué frontmatter lleva cada uno y cómo corre el flujo spec-driven.
2. **Memoria del proyecto** — el estado vivo de UMBRAL: dónde estamos, qué se decidió y qué sigue (§7).

> **Jerarquía de verdad.** Si dos documentos se contradicen, manda en este orden: `marca/MARCA_UMBRAL.md` → `producto/UMBRAL_PRODUCTO.md` → specs de la feature → el resto. La marca gana siempre.

---

## 1. Para qué sirve el CKM

- **Una sola fuente de verdad.** Nada de conocimiento disperso en chats, mails o cabezas. Lo que no está en el CKM, no existe a efectos del proyecto.
- **Spec-driven design.** No se escribe código sin spec. La spec es el contrato; el código la implementa. Ver §5.
- **Legible por agentes de AI.** El naming jerárquico y el frontmatter permiten que un agente filtre y navegue sin ambigüedad. Por eso las convenciones no son opcionales.
- **Coherencia de marca.** UMBRAL es una marca antes que un software. Cada documento se valida contra `MARCA_UMBRAL.md` (ver §6).

---

## 2. Estructura de carpetas

```
CKM/
├── README.md            ← este documento: guía + memoria del proyecto
│
├── marca/               ← identidad de UMBRAL — la fuente de verdad máxima
│   ├── MARCA_UMBRAL.md                 (biblia de marca)
│   └── MANUAL_DE_MARCA_… .pdf          (manual original)
│
├── producto/            ← el "qué" y el "para qué" del producto
│   └── UMBRAL_PRODUCTO.md              (documento de bases)
│
├── SPECS/               ← spec-driven design (el "cómo se construye")
│   ├── README.md                       (índice del flujo + gates)
│   ├── _templates/                     (los 9 templates base, no se editan)
│   └── <feature-slug>/                 (una carpeta por feature, se crea al arrancarla)
│
├── diseño/              ← design system, wireframes, tokens, assets visuales
├── software/            ← arquitectura, modelo de datos, deploy, seguridad
└── negocio/             ← comercial, pricing, go-to-market, métricas
```

Cada carpeta tiene su propio `README.md` que explica qué vive ahí. `marca/`, `producto/` y `SPECS/` ya tienen contenido; `diseño/`, `software/` y `negocio/` arrancan como placeholders y se llenan a medida que el proyecto lo pide.

### Áreas (vocabulario controlado)

| Área | Carpeta | Qué contiene |
|---|---|---|
| `marca` | `marca/` | Biblia de marca, identidad visual, tono de voz, manual. **Gana sobre todo.** |
| `producto` | `producto/` | Visión, bases del producto, alcance, decisiones de producto. |
| `specs` | `SPECS/` | Especificaciones del flujo spec-driven (las 9 fases). |
| `diseño` | `diseño/` | Design system, wireframes, mockups, tokens, copy de UI. |
| `software` | `software/` | Arquitectura, modelo de datos, integraciones, deploy, seguridad. |
| `negocio` | `negocio/` | Comercial, pricing, go-to-market, métricas de negocio. |

---

## 3. Naming de archivos

Dos convenciones, según el tipo de archivo:

### 3.1 Documentos de conocimiento (`area.subtema.nombre.md`)

Tres niveles separados por puntos. Permite al agente navegar por jerarquía sin leer el contenido.

```
[area].[subtema].[nombre-especifico].md
```

Ejemplos:

| Archivo | Contenido |
|---|---|
| `software.arquitectura.overview.md` | Visión general del sistema y stack. |
| `software.arquitectura.modelo-datos.md` | Schema de DB y aislamiento por membresía. |
| `diseño.sistema.tokens.md` | Tokens de color, tipografía, espaciado. |
| `diseño.sistema.componentes.md` | Inventario de componentes UI. |
| `negocio.comercial.pricing.md` | Estructura de fee por proyecto / suscripción. |
| `producto.decisiones.log.md` | Bitácora de decisiones de producto. |

> Los dos documentos fundacionales (`MARCA_UMBRAL.md`, `UMBRAL_PRODUCTO.md`) conservan su nombre histórico por ser raíz del proyecto y estar muy referenciados. Todo documento nuevo sigue la convención `area.subtema.nombre.md`.

### 3.2 Specs de una feature (dentro de `SPECS/<feature-slug>/`)

Cada feature vive en su propia carpeta con slug en kebab-case. Adentro, un archivo por fase, con el nombre de la fase:

```
SPECS/onboarding-inversor/
├── Discovery-Spec.md
├── PRD-Spec.md
├── Design-Spec.md
├── Technical-Spec.md
├── API-Spec.md
├── Test-Spec.md
├── Implementation-Spec.md
├── Validation-Spec.md
└── Release-Spec.md
```

Para arrancar una feature: copiar los templates de `SPECS/_templates/` a `SPECS/<feature-slug>/`. Ver `SPECS/README.md`.

---

## 4. Frontmatter

Cada `.md` arranca con un bloque YAML entre `---`. Es lo que permite a un agente filtrar antes de leer.

```yaml
---
title: "Título descriptivo del documento"
area: software          # marca | producto | specs | diseño | software | negocio
audiencia: interno      # interno | desarrollador | inversor
tipo: spec              # spec | template | politica | proceso | referencia | vision | faq
sensibilidad: interno   # publico | interno | confidencial
owner: "@usuario-github"
estado: borrador        # borrador | vigente | deprecado
revision-cada: "90d"
ultima-revision: "2026-06-08"
tags: [tag1, tag2, tag3]
relacionado: []
---
```

### Campos extra para specs (`tipo: spec` / `tipo: template`)

```yaml
feature-status: backlog   # backlog | en-desarrollo | completado
pr-relacionado: ""
```

### Vocabulario de cada campo

| Campo | Valores | Notas |
|---|---|---|
| `area` | marca · producto · specs · diseño · software · negocio | 1 por documento. |
| `audiencia` | `interno` (equipo UMBRAL) · `desarrollador` (cliente B2B que paga) · `inversor` (usuario final de la app) | 1 o más. |
| `tipo` | spec · template · politica · proceso · referencia · vision · faq | 1 por documento. |
| `sensibilidad` | `publico` (puede salir a landing/redes) · `interno` (solo equipo) · `confidencial` (negocios privados, fees, Banca — ver MARCA §16) | 1 por documento. |
| `estado` | borrador · vigente · deprecado | — |

> **Sensibilidad `confidencial`:** todo lo que la marca prohíbe comunicar en público (topes, comisiones, fees, reglas de Banca, mecánicas de remate — `MARCA_UMBRAL.md` §16) va marcado así.

---

## 5. El flujo spec-driven (9 fases + 2 gates)

UMBRAL se construye en 9 fases secuenciales con 2 gates de control. El detalle operativo vive en `SPECS/README.md`; acá el mapa:

| # | Fase | Template |
|---|---|---|
| 1 | Discovery | `Discovery-Spec.md` |
| 2 | Requirements (PRD) | `PRD-Spec.md` |
| 3 | Design Spec | `Design-Spec.md` |
| — | 🚪 **Gate 1 — Alineación de stakeholders + marca** | — |
| 4 | Technical Spec | `Technical-Spec.md` |
| 5 | API / Contract Spec | `API-Spec.md` |
| 6 | Test Spec | `Test-Spec.md` |
| — | 🚪 **Gate 2 — Tech review y sign-off** | — |
| 7 | Plan de Implementación | `Implementation-Spec.md` |
| 8 | Reporte de Validación | `Validation-Spec.md` |
| 9 | Release y Evolución | `Release-Spec.md` |

**Regla de oro:** la spec es la fuente de verdad. Si la implementación diverge de la spec, primero se actualiza la spec (spec amendment), después se mergea el código.

---

## 6. Consideraciones propias de UMBRAL (no opcionales)

Lo que en una fintech serían CNV/UIF/KYC, en UMBRAL son dos cosas: **la marca** y **el aislamiento de datos**. Toda spec las evalúa.

### 6.1 Alineación de marca

`MARCA_UMBRAL.md` gana sobre cualquier spec. Antes de cerrar Discovery, PRD y Design:

- **Palabras prohibidas en UI y copy externo** (MARCA §3, §10): *postventa / posventa, CRM, comunicador, atención al cliente, soporte* (como descripción de UMBRAL), *promesa*. Usar el vocabulario de reemplazo (MARCA §10, `UMBRAL_PRODUCTO.md` §6).
- **Idioma:** español rioplatense, voseo. Tono sobrio, cálido, arquitectónico, frases cortas.
- **No prometer tech que no existe** (ej: "tiempo real" si no lo hay).
- El **Copy Deck** de toda Design Spec se revisa contra la marca antes del Gate 1.

### 6.2 Aislamiento por membresía (inversor × desarrollo)

Requisito de seguridad estructural (`UMBRAL_PRODUCTO.md` §2, §5). Cada inversor ve **únicamente** sus desarrollos; lo enforcea el backend, no el front.

- Toda feature que toque datos de inversor lleva casos `TC-SEC-*` de aislamiento en su Test Spec (un inversor no puede acceder al desarrollo de otro).
- El backoffice respeta roles: **Admin UMBRAL** (todos los desarrollos) vs **Admin desarrollador** (solo los suyos).

### 6.3 Dos frontends, un backend

UMBRAL son dos productos sobre un backend compartido: **app del inversor** (mobile-first) y **backoffice** (desktop). Las specs distinguen siempre a cuál de los dos aplican.

---

## 7. Memoria del proyecto — estado vivo

> Sección que se actualiza seguido. Es el "dónde estamos" de UMBRAL. Convertir fechas relativas a absolutas.

### 7.1 Snapshot

- **Etapa actual:** documentación pre-desarrollo. Sentando bases antes de diseñar y construir.
- **Fecha de este snapshot:** 2026-06-08.
- **Documentos fundacionales listos:** `MARCA_UMBRAL.md` (biblia de marca, vigente) y `UMBRAL_PRODUCTO.md` (bases de producto, en refinamiento).
- **Estructura del CKM:** creada (este commit).

### 7.2 Qué es UMBRAL en una línea

> Una nueva capa de valor para desarrolladores: acompaña al inversor entre la firma y la entrega, eleva la imagen del desarrollador durante la obra y convierte la experiencia en recompra y referido. **No es postventa, no es CRM, no es un comunicador.**

### 7.3 Próximos pasos acordados

1. ✅ Crear el esquema de orden del CKM, este README y los templates base. **(hecho)**
2. ⬜ Refinar `producto/UMBRAL_PRODUCTO.md`.
3. ⬜ Empezar a llenar las specs (arrancando por Discovery de la primera feature de la v1).

### 7.4 Decisiones abiertas (heredadas de UMBRAL_PRODUCTO.md §8)

- **Login:** ¿Google + email en v1 o solo email primero?
- **Código de referencia:** ¿1 código por inversor o 1 por desarrollo?
- **Validación de m²:** ¿declara el inversor y confirma UMBRAL, o entra directo?
- **Recordatorios de pago:** ¿solo aviso o integración con cobranza del desa?
- **Roles del desarrollador en backoffice:** ¿read-only o puede cargar contenido?

### 7.5 Bitácora de cambios del CKM

| Fecha | Cambio |
|---|---|
| 2026-06-08 | Estructura inicial del CKM: carpetas `marca/`, `producto/`, `SPECS/`, `diseño/`, `software/`, `negocio/`; este README; 9 templates de spec. Docs fundacionales reubicados. |

---

*Mantené este documento vivo. Cuando algo cambie en el rumbo del proyecto, se actualiza acá antes que en ningún otro lado.*
