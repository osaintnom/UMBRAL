---
title: "Impl Plan: [nombre de la feature]"
area: specs
audiencia: interno
tipo: spec
sensibilidad: interno
owner: "@"
estado: borrador
revision-cada: "30d"
ultima-revision: ""
feature-status: en-desarrollo
pr-relacionado: ""
tags: [spec, implementacion]
relacionado: []
---

# Plan de Implementación — [Nombre de la Feature]

**Technical Spec relacionada:** `Technical-Spec`
**Test Spec relacionada:** `Test-Spec`
**Sprint / milestone:** [nombre o número]

---

## 1. Descomposición en Tickets

> Cada ticket = una unidad que puede revisarse y mergearse por separado.
> Dependencias explícitas.

### Backend (compartido)

| Ticket | Descripción | Depende de | Estimación | Asignado a |
|--------|-------------|-----------|-----------|------------|
| BE-01 | Migration: [nombre] | — | | |
| BE-02 | Modelo y repositorio: [entidad] | BE-01 | | |
| BE-03 | Servicio: [lógica de negocio] | BE-02 | | |
| BE-04 | Enforcement de aislamiento por membresía | BE-02 | | |
| BE-05 | Endpoint: POST /[recurso] | BE-03, BE-04 | | |
| BE-06 | Endpoint: GET /[recurso] | BE-03, BE-04 | | |
| BE-07 | Tests unitarios y de integración (incl. aislamiento) | BE-05, BE-06 | | |

### Frontend — App del inversor (mobile-first)

| Ticket | Descripción | Depende de | Estimación | Asignado a |
|--------|-------------|-----------|-----------|------------|
| APP-01 | Componente: [nombre] (contra mock server) | — | | |
| APP-02 | Pantalla: [nombre] — happy path | APP-01 | | |
| APP-03 | Pantalla: [nombre] — estados de error/vacío | APP-02 | | |
| APP-04 | Integración con API real (reemplazar mocks) | BE-05, APP-03 | | |

### Frontend — Backoffice (desktop)

| Ticket | Descripción | Depende de | Estimación | Asignado a |
|--------|-------------|-----------|-----------|------------|
| BO-01 | Vista: [nombre] (contra mock server) | — | | |
| BO-02 | Integración con API real | BE-06, BO-01 | | |

### Infra / DevOps (si aplica)

| Ticket | Descripción | Depende de | Estimación | Asignado a |
|--------|-------------|-----------|-----------|------------|
| INF-01 | | | | |

---

## 2. Orden de Ejecución y Paralelismo

```
Sprint 1:
  BE-01 (migration) ───────────────────────────►
  APP-01 / BO-01 (UI contra mock) ──────────────►

Sprint 2:
  BE-02 ──► BE-03, BE-04 ──► BE-05, BE-06 ───────►
  APP-02 ──► APP-03 ─────────────────────────────►

Sprint 3:
  APP-04 / BO-02 (integración) ──► BE-07 ────────►
```

---

## 3. Reglas de Implementación

### La spec es la fuente de verdad
- Antes de implementar un caso no cubierto en la spec, agregar el coverage a la spec.
- Si la spec y la realidad técnica chocan, abrir un spec amendment (§4) antes de mergear.
- El reviewer verifica que el código implementa lo que dice la spec.

### Estándares de UMBRAL
- Seguir las convenciones de `software.arquitectura.overview`.
- **Aislamiento:** ningún endpoint devuelve datos fuera de la membresía del usuario. Cubierto por tests (TC-SEC-03/04).
- **Marca:** todo copy nuevo coincide con el Copy Deck aprobado (voseo, sin palabras prohibidas). No introducir texto visible sin pasar por la Design Spec.
- Nunca loggear datos personales del inversor en texto plano.

### Checklist de cada PR
- [ ] Referencia el ticket (BE-/APP-/BO-/INF-XX)
- [ ] Referencia la sección de la spec que implementa
- [ ] Tests escritos y pasando en CI
- [ ] Sin datos sensibles en logs ni en respuestas de error
- [ ] Si hay copy visible: coincide con el Copy Deck aprobado
- [ ] Si hay cambio de comportamiento observable: la spec se actualizó primero

---

## 4. Spec Amendments

> Registro de divergencias entre la spec original y lo implementado.
> Cada amendment se aprueba antes de mergear.

**SA-[número] — [Título]**
- **Ticket relacionado:**
- **Sección de spec afectada:**
- **Qué dice la spec:**
- **Qué se encontró en la implementación:**
- **Propuesta alternativa:**
- **Aprobado por:** @producto — @tech — Fecha: ____
- **Spec actualizada:** sí / no

*(Registrar amendments acá a medida que surgen)*

---

## 5. Changelog de la Feature

> Una línea por cambio relevante, en lenguaje comprensible para stakeholders no técnicos.

| Fecha | Cambio | Ticket |
|-------|--------|--------|
| | | |

---

## 6. Criterio de Salida de Implementación

- [ ] Todos los tickets Must y Should implementados y mergeados
- [ ] Sin divergencias no documentadas entre spec y código
- [ ] Todos los PRs con code review aprobado
- [ ] Tests automatizados para todos los AC Must, incluyendo aislamiento
- [ ] Sin datos sensibles expuestos en logs ni respuestas
- [ ] Copy visible coincide con el Copy Deck
- [ ] Spec actualizada con los spec amendments aprobados
- [ ] Changelog actualizado

---

*Siguiente paso: completar `Validation-Spec.md`*
