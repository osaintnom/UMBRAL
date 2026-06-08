---
title: "PRD: [nombre de la feature]"
area: specs
audiencia: interno
tipo: spec
sensibilidad: interno
owner: "@"
estado: borrador
revision-cada: "30d"
ultima-revision: ""
feature-status: backlog
pr-relacionado: ""
tags: [spec, prd, requirements]
relacionado: []
---

# PRD — [Nombre de la Feature]

**Versión:** 1.0
**Estado:** Borrador / En revisión / Aprobado
**Discovery relacionado:** `Discovery-Spec`
**Aplica a:** ⬜ App del inversor · ⬜ Backoffice · ⬜ Backend

---

## 1. Resumen Ejecutivo

> Una o dos oraciones: qué hace la feature y por qué existe ahora.
> Describí qué valor entrega, no cómo funciona internamente.

---

## 2. Contexto

**Problema que resuelve:**
> Referencia al problem statement del Discovery. No reescribir, referenciar.

**Por qué ahora:**
> Qué cambió en el producto, el mercado o los usuarios que hace que esta feature sea prioritaria.

---

## 3. Usuarios Objetivo

| Segmento | Descripción | Frecuencia de uso esperada |
|----------|-------------|---------------------------|
| Inversor | | |
| Desarrollador / Admin desarrollador | | |
| Equipo UMBRAL | | |

---

## 4. Casos de Uso Principales

> Cada caso desde la perspectiva del usuario, en lenguaje natural.
> Numerados por importancia, no por flujo técnico.

**CU-01 — [Nombre del caso]**
Como [tipo de usuario], quiero [acción] para [resultado].

**CU-02 — [Nombre del caso]**
Como [tipo de usuario], quiero [acción] para [resultado].

**CU-03 — [Nombre del caso]**
Como [tipo de usuario], quiero [acción] para [resultado].

---

## 5. Requisitos Funcionales

> Formato: ID | Descripción | Prioridad | Acceptance Criteria
> Prioridad: Must / Should / Could / Won't (MoSCoW)

### 5.1 Must Have

#### RF-01 — [Nombre del requisito]
**Descripción:** Qué debe hacer el sistema.
**Prioridad:** Must

**Acceptance Criteria:**
- **AC-01a:** GIVEN [contexto / precondición]
  WHEN [acción del usuario o evento del sistema]
  THEN [resultado esperado — concreto y verificable]

- **AC-01b:** GIVEN [contexto]
  WHEN [acción]
  THEN [resultado]

---

#### RF-02 — [Nombre del requisito]
**Descripción:**
**Prioridad:** Must

**Acceptance Criteria:**
- **AC-02a:** GIVEN
  WHEN
  THEN

---

### 5.2 Should Have

#### RF-03 — [Nombre del requisito]
**Descripción:**
**Prioridad:** Should

**Acceptance Criteria:**
- **AC-03a:** GIVEN
  WHEN
  THEN

---

### 5.3 Could Have

#### RF-04 — [Nombre del requisito]
**Descripción:**
**Prioridad:** Could

---

### 5.4 Won't Have (este ciclo)

- [Funcionalidad excluida explícitamente] — Razón:
- [Funcionalidad excluida explícitamente] — Razón:

---

## 6. Requisitos No Funcionales

### Performance
| Requisito | Target | Método de verificación |
|-----------|--------|----------------------|
| Latencia de endpoints críticos | P95 < 300ms | Test de carga |
| Tiempo de carga de pantallas (app mobile) | < 2s en 3G | Lighthouse en CI |

### Seguridad y aislamiento
> El aislamiento por (inversor × desarrollo) es requisito estructural de UMBRAL.

- [ ] Autenticación requerida: sí / no
- [ ] Roles con acceso: inversor / admin desarrollador / admin UMBRAL / todos
- [ ] ¿Toca datos de inversores? → debe respetar el aislamiento por membresía (`UMBRAL_PRODUCTO.md` §5)
- [ ] ¿El backoffice distingue Admin UMBRAL (todo) vs Admin desarrollador (lo suyo)?
- [ ] Validación de inputs

### Alineación de Marca
- [ ] Todo copy visible usa voseo rioplatense y tono sobrio/arquitectónico
- [ ] Sin palabras prohibidas (postventa, CRM, comunicador, soporte, atención al cliente, promesa)
- [ ] Nada promete comportamiento inexistente

### Disponibilidad
| Requisito | Target |
|-----------|--------|
| Uptime | |

### Accesibilidad
- Nivel WCAG: AA
- Mobile-first (app del inversor): sí / no
- Soporte para lectores de pantalla: sí / no

---

## 7. Out of Scope

> Lo que esta feature NO incluye en este ciclo. Si no está acá, puede interpretarse como incluido.

- [Item] — Se pospone porque:
- [Item] — Se pospone porque:
- [Item] — Se pospone porque:

---

## 8. Dependencias

| Dependencia | Tipo | Estado | Doc de referencia |
|-------------|------|--------|-------------------|
| | técnica / de producto / de marca | en progreso / bloqueante / resuelta | |

---

## 9. Métricas de Éxito

> Copiadas del Discovery para que el PRD sea autocontenido.

**Métrica primaria:** [métrica] → target [valor] en [timeframe]
**Guardrails:** [métrica que no debe empeorar]

---

## 10. Historial de Revisiones

| Versión | Fecha | Autor | Cambios |
|---------|-------|-------|---------|
| 1.0 | | | Borrador inicial |

---

## 11. Criterio de Salida del PRD

- [ ] Todos los requisitos Must tienen acceptance criteria en formato Given-When-Then
- [ ] Out of scope documentado con al menos 3 ítems
- [ ] Dependencias identificadas con estado
- [ ] Requisitos de seguridad/aislamiento evaluados
- [ ] Requisitos de marca evaluados (voseo, palabras prohibidas, honestidad)
- [ ] Revisado por quien implementa
- [ ] Sign-off de producto: @_____ — Fecha: ____
- [ ] Sign-off del stakeholder principal: @_____ — Fecha: ____
- [ ] Versionado como PRD v1.0

---

*Siguiente paso: completar `Design-Spec.md`*
