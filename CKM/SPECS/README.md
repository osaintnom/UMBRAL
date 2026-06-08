---
title: "Spec-Driven Design UMBRAL — índice de templates y flujo"
area: specs
audiencia: interno
tipo: proceso
sensibilidad: interno
owner: "@santiromero1"
estado: vigente
revision-cada: "180d"
ultima-revision: "2026-06-08"
tags: [spec, proceso, templates, gates]
relacionado: [../README.md, ../marca/MARCA_UMBRAL.md, ../producto/UMBRAL_PRODUCTO.md]
---

# Spec-Driven Design — UMBRAL

UMBRAL se construye con spec-driven design: **no se escribe código sin spec**. La spec es el contrato; el código la implementa. Esta carpeta contiene los templates de las 9 fases y la guía para usarlos.

---

## Cómo arrancar una feature

1. Elegí un slug en kebab-case para la feature (ej: `onboarding-inversor`, `home-valorizacion`, `vender-unidad`, `backoffice-altas`).
2. Creá la carpeta `SPECS/<feature-slug>/`.
3. Copiá los templates que necesites desde `_templates/` a esa carpeta.
4. Completá fase por fase, respetando los gates.

```bash
# ejemplo
mkdir -p SPECS/onboarding-inversor
cp SPECS/_templates/*.md SPECS/onboarding-inversor/
```

Resultado:

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

> Los archivos en `_templates/` **no se editan** — son la plantilla base. Se copian y se completan en la carpeta de la feature.

---

## Las 9 fases y sus templates

| # | Fase | Template | feature-status al crear |
|---|------|----------|------------------------|
| 1 | Discovery | `Discovery-Spec.md` | backlog |
| 2 | Requirements (PRD) | `PRD-Spec.md` | backlog |
| 3 | Design Spec | `Design-Spec.md` | backlog |
| — | 🚪 **Gate 1 — Alineación de stakeholders + marca** | — | — |
| 4 | Technical Spec | `Technical-Spec.md` | backlog |
| 5 | API / Contract Spec | `API-Spec.md` | backlog |
| 6 | Test Spec | `Test-Spec.md` | backlog |
| — | 🚪 **Gate 2 — Tech review y sign-off** | — | — |
| 7 | Plan de Implementación | `Implementation-Spec.md` | en-desarrollo |
| 8 | Reporte de Validación | `Validation-Spec.md` | en-desarrollo |
| 9 | Release y Evolución | `Release-Spec.md` | completado |

---

## Reglas de frontmatter por fase

### feature-status
Actualizar `feature-status` en **todos** los docs de la feature al avanzar:
- Fases 1–6: `backlog`
- Fases 7–8: `en-desarrollo`
- Fase 9 y post-lanzamiento: `completado`

### estado
- Mientras se escribe: `borrador`
- Tras el sign-off de la fase: `vigente`
- Si la feature se reemplaza o descontinúa: `deprecado`

### relacionado
Enlazar los demás docs de la misma feature:
```yaml
relacionado:
  - SPECS/onboarding-inversor/Discovery-Spec
  - SPECS/onboarding-inversor/PRD-Spec
  - ../../marca/MARCA_UMBRAL.md
```

---

## Los gates

### 🚪 Gate 1 — Alineación de stakeholders + marca (entre fase 3 y 4)
Antes de pasar a las specs técnicas:
- [ ] PRD v1.0 firmado por el responsable de producto y stakeholders.
- [ ] Design Spec aprobada (producto + quien implemente).
- [ ] **Copy y nombres validados contra `MARCA_UMBRAL.md`**: sin palabras prohibidas (postventa, CRM, comunicador, soporte, atención al cliente, promesa), voseo rioplatense, tono sobrio/arquitectónico.
- [ ] Definido a cuál producto aplica: **app del inversor** (mobile-first) y/o **backoffice** (desktop).
- [ ] Sin preguntas abiertas que bloqueen el trabajo técnico.

### 🚪 Gate 2 — Tech review y sign-off (entre fase 6 y 7)
Antes de implementar:
- [ ] Technical Spec aprobada.
- [ ] API Spec completa y validada.
- [ ] Test Spec cubre todos los AC Must y Should.
- [ ] **Aislamiento por membresía cubierto** con casos `TC-SEC-*` (un inversor no accede al desarrollo de otro).
- [ ] Mock server / datos de prueba disponibles para arrancar frontend en paralelo.

---

## Consideraciones propias de UMBRAL (en toda feature)

### Marca primero
`MARCA_UMBRAL.md` gana sobre cualquier spec. El Copy Deck de la Design Spec se revisa contra la marca antes del Gate 1. Palabras prohibidas y vocabulario de reemplazo: ver `../README.md` §6 y `MARCA_UMBRAL.md` §10.

### Aislamiento por (inversor × desarrollo)
Cada inversor ve solo sus desarrollos; lo enforcea el backend. Toda feature que toque datos de inversor lleva `TC-SEC-*` de aislamiento en su Test Spec. Roles del backoffice: **Admin UMBRAL** (todos) vs **Admin desarrollador** (los suyos).

### Dos frontends, un backend
Cada spec aclara si aplica a la **app del inversor**, al **backoffice**, o a ambos. Ver `../producto/UMBRAL_PRODUCTO.md` §2.

### Honestidad técnica
No documentar ni prometer comportamiento que no existe (ej: "tiempo real"). La marca lo prohíbe (MARCA §10).
