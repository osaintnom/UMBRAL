---
title: "Validation Report: [nombre de la feature]"
area: specs
audiencia: interno
tipo: proceso
sensibilidad: interno
owner: "@"
estado: borrador
revision-cada: "30d"
ultima-revision: ""
feature-status: en-desarrollo
pr-relacionado: ""
tags: [spec, validation, qa]
relacionado: []
---

# Reporte de Validación — [Nombre de la Feature]

**Test Spec relacionada:** `Test-Spec`
**Entorno validado:** `staging.umbral.app`
**Fecha de inicio:** ____
**Fecha de cierre:** ____

---

## 1. Resumen Ejecutivo

| Métrica | Resultado |
|---------|-----------|
| Test cases ejecutados | [X] de [total] |
| Test cases Pass | |
| Test cases Fail | |
| Test cases Blocked | |
| Defectos Blocker | |
| Defectos Major | |
| Defectos Minor | |
| Listo para lanzar | ✅ Sí / ❌ No — Motivo: |

---

## 2. Resultados de Tests Automatizados

### Tests unitarios y de integración
- **Fecha:** ____
- **Resultado:** ✅ Todos pasan / ❌ [X] fallando
- **Link al run de CI:** [URL]

### Tests de contrato (API spec)
- **Herramienta:** Dredd / Pact
- **Resultado:** ✅ / ❌
- **Detalles:** [endpoints con discrepancia]

### Tests de performance
- **Herramienta:** k6
- **Fecha:** ____

| Endpoint | P95 obtenido | P95 target | P99 obtenido | P99 target | Resultado |
|----------|-------------|-----------|-------------|-----------|-----------|
| `POST /[recurso]` | | 300ms | | 600ms | ✅ / ❌ |
| `GET /[recurso]` | | 200ms | | 400ms | ✅ / ❌ |

### Tests de accesibilidad
- **Herramienta:** axe-core
- **Resultado:** ✅ 0 violations / ❌ [X] violations

---

## 3. Ejecución de Test Cases Manuales

| ID | Descripción | Prioridad | Resultado | Defecto | Ejecutado por |
|----|-------------|-----------|-----------|---------|--------------|
| TC-[FLUJO]-01 | | Alta | ✅ / ❌ / ⏸ | | |
| TC-SEC-01 | Acceso sin autenticación | Alta | | | |
| TC-SEC-03 | Inversor accede al desarrollo de otro | Alta | | | |
| TC-SEC-04 | Admin desa accede a desarrollo de otro | Alta | | | |
| TC-MARCA-01 | Sin palabras prohibidas en UI | Alta | | | |

---

## 4. Registro de Defectos

### Blocker — [cantidad]

#### BUG-[número] — [Título]
**Ticket:** [link]
**Severidad:** Blocker
**Estado:** Abierto / En progreso / Resuelto

**Pasos para reproducir:**
1.
2.

**Resultado actual:**

**Resultado esperado (según spec):**

**Sección de spec afectada:** [fase]-Spec — sección [X]

**Evidencia:** [link a screenshot o video]

---

### Major — [cantidad]

*(mismo formato que Blocker)*

---

### Minor y cosmético — [cantidad]

| ID | Descripción | Decisión: fix ahora / backlog |
|----|-------------|-------------------------------|
| | | |

---

## 5. UAT (si aplica)

> Completar si la feature afecta al inversor o al desarrollador.

**Participantes:**
| Nombre | Rol | Desarrollo / empresa |
|--------|-----|----------------------|
| | Inversor representativo | |
| | Admin desarrollador | |

**Fecha:** ____

### Findings del UAT
| Finding | Severidad para el lanzamiento | Acción |
|---------|------------------------------|--------|
| | Bloqueante / No bloqueante | |

**Conclusión:**
> ✅ Satisfactorio / ❌ Con observaciones (ver findings)

---

## 6. Sign-off de Lanzamiento

### QA Sign-off
**Estado:** ✅ Aprobado / ❌ Pendiente
**Condiciones:** Sin defectos Blocker ni Major abiertos. Todos los TC de prioridad Alta en Pass. Todos los TC-SEC-* en Pass.
**@QA:** _____ — Fecha: ____

### Producto Sign-off
**Estado:** ✅ Aprobado / ❌ Pendiente
**Condiciones:** Los acceptance criteria del PRD se cumplen. UAT satisfactorio.
**@Producto:** _____ — Fecha: ____

### Tech Sign-off
**Estado:** ✅ Aprobado / ❌ Pendiente
**Condiciones:** Implementación correcta, segura (aislamiento garantizado), sin deuda técnica no documentada.
**@Tech:** _____ — Fecha: ____

### Marca Sign-off (si hubo copy nuevo)
**Estado:** ✅ Aprobado / ❌ Pendiente / N/A
**Condiciones:** Copy en voseo, sin palabras prohibidas, sin promesas de tech inexistente.
**@Marca:** _____ — Fecha: ____

---

## 7. Criterio de Salida de Validación

- [ ] Todos los tests automatizados pasan en staging
- [ ] Tests de performance dentro de los targets de la Test Spec
- [ ] Todos los TC de prioridad Alta en Pass
- [ ] Todos los TC-SEC-* (aislamiento) en Pass
- [ ] TC-MARCA-* en Pass
- [ ] No hay defectos Blocker abiertos
- [ ] No hay defectos Major abiertos (o están aceptados con justificación)
- [ ] UAT completado y findings resueltos o clasificados como no bloqueantes
- [ ] Los sign-offs están firmados (Marca N/A si no hubo copy nuevo)

---

*Siguiente paso: completar `Release-Spec.md`*
