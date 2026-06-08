---
title: "Test Spec: [nombre de la feature]"
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
tags: [spec, testing, qa]
relacionado: []
---

# Test Spec — [Nombre de la Feature]

**PRD relacionado:** `PRD-Spec`
**API Spec relacionada:** `API-Spec`
**Entorno de test:** `staging.umbral.app` *(placeholder — ajustar)*

---

## 1. Alcance

**Cubre:**
- [Flujo o módulo que se testea]

**Fuera de alcance:**
- [Funcionalidad no cubierta] — cubierta en [referencia]

---

## 2. Criterios de Aceptación (fuente: PRD)

| ID AC | Descripción | Prioridad |
|-------|-------------|-----------|
| AC-01a | GIVEN... WHEN... THEN... | Must |
| AC-01b | GIVEN... WHEN... THEN... | Must |
| AC-02a | | Should |

---

## 3. Casos de Prueba

### 3.1 [Nombre del flujo principal]

---

**TC-[FLUJO]-01 — [Descripción del happy path]**
*Cubre: AC-[ID]*
*Prioridad: Alta*
*Tipo: Funcional / E2E*

**Precondición:**
- Usuario: [inversor con membresía activa / admin desarrollador / admin UMBRAL]
- Estado del sistema: [ej: el inversor tiene al menos 1 desarrollo]

**Pasos:**
1.
2.
3.

**Resultado esperado:**
- HTTP [status] (si es test de API)
- [Comportamiento esperado en la UI]
- [Dato persistido o evento generado]

---

**TC-[FLUJO]-02 — [Descripción del error más probable]**
*Cubre: AC-[ID] (escenario negativo)*
*Prioridad: Alta*

**Precondición:**

**Pasos:**
1.
2.

**Resultado esperado:**
- Mensaje de error: "[texto exacto del Copy Deck]"
- No se genera ningún registro en la base de datos
- El usuario puede reintentar sin recargar

---

**TC-[FLUJO]-03 — [Escenario de borde]**
*Cubre: AC-[ID]*
*Prioridad: Media*

*(Repetir por cada caso de prueba)*

---

### 3.2 Casos de seguridad y aislamiento

> Críticos en UMBRAL: el aislamiento por (inversor × desarrollo) es estructural.

---

**TC-SEC-01 — Acceso sin autenticación**
*Prioridad: Alta*

**Pasos:**
1. Request a `[endpoint]` sin header `Authorization`

**Resultado esperado:**
- HTTP `401 Unauthorized`
- No se devuelve ningún dato

---

**TC-SEC-02 — Acceso con rol insuficiente**
*Prioridad: Alta*

**Pasos:**
1. Autenticarse como [inversor / admin desarrollador]
2. Intentar una acción que requiere [rol superior, ej: admin UMBRAL]

**Resultado esperado:**
- HTTP `403 Forbidden`
- No se revela información del recurso protegido

---

**TC-SEC-03 — Inversor accede al desarrollo de otro (aislamiento)**
*Prioridad: Alta*
> El caso más importante de UMBRAL.

**Pasos:**
1. Autenticarse como Inversor A (membresía en Desarrollo X)
2. Intentar acceder a un recurso del Desarrollo Y usando su ID

**Resultado esperado:**
- HTTP `404 Not Found` (no revelar que el recurso existe)
- No se devuelve ningún dato del Desarrollo Y

---

**TC-SEC-04 — Admin desarrollador accede al desarrollo de otro desarrollador**
*Prioridad: Alta*

**Pasos:**
1. Autenticarse como Admin del Desarrollador A
2. Intentar acceder a datos de un desarrollo del Desarrollador B

**Resultado esperado:**
- HTTP `404 Not Found`
- No se devuelven datos del Desarrollador B

---

**TC-SEC-05 — Inputs con caracteres maliciosos**
*Prioridad: Alta*

| Input | Resultado esperado |
|-------|-------------------|
| `<script>alert(1)</script>` en campo texto | `400/422` — validation_error |
| SQL injection en parámetro de búsqueda | `400/422` — validation_error |

---

### 3.3 Casos de marca (copy y tono)

> Sección propia de UMBRAL: el texto visible respeta la marca.

**TC-MARCA-01 — Sin palabras prohibidas en UI**
*Prioridad: Alta*

**Resultado esperado:**
- Ningún texto visible usa: postventa/posventa, CRM, comunicador, soporte (como descripción de UMBRAL), atención al cliente, promesa.

**TC-MARCA-02 — Voseo y tono**
*Prioridad: Media*

**Resultado esperado:**
- Todo el copy está en voseo rioplatense, tono sobrio/arquitectónico, coincide con el Copy Deck aprobado.

---

## 4. Tests No Funcionales

### 4.1 Performance

**Herramienta:** k6 (o equivalente)
**Escenario:** [X] usuarios virtuales concurrentes durante [X] minutos

| Endpoint | P95 target | P99 target | Throughput mínimo |
|----------|-----------|-----------|-------------------|
| `POST /[recurso]` | 300ms | 600ms | [X] req/s |
| `GET /[recurso]` | 200ms | 400ms | [X] req/s |

### 4.2 Seguridad

| Check | Método | Resultado esperado |
|-------|--------|-------------------|
| Tokens no aparecen en logs | Revisión manual de logs en staging | Sin datos sensibles |
| Datos de inversores no se exponen en errores | TC-SEC-01 a TC-SEC-05 | Solo mensajes genéricos |
| Aislamiento entre desarrollos | TC-SEC-03, TC-SEC-04 | Sin fugas |
| HTTPS obligatorio | `curl http://[endpoint]` | Redirección a HTTPS |

### 4.3 Accesibilidad

| Check | Herramienta | Criterio |
|-------|-------------|---------|
| Sin errores de nivel AA | axe-core en CI | 0 violations críticas |
| Formularios con labels asociados | Inspección manual | Todos los campos con `<label>` |
| Navegable por teclado | Inspección manual | Tab/Enter/Escape funcionan |

---

## 5. Datos de Prueba

**Entorno:** `staging.umbral.app`
**Script de seed:** `scripts/seed-[nombre-feature].sh`

### Usuarios de prueba

| Rol | Email | Estado | Notas |
|-----|-------|--------|-------|
| Inversor (Desarrollo X) | `test-inversor-x@umbral.app` | Membresía activa, m² cargados | |
| Inversor multi-desarrollo | `test-inversor-multi@umbral.app` | Membresía en 2 desarrollos | |
| Admin desarrollador A | `test-admindesa-a@umbral.app` | Solo Desarrollo X | |
| Admin UMBRAL | `test-adminumbral@umbral.app` | Todos los desarrollos | |

### Estados de datos necesarios

| Estado | Cómo crearlo | Nota |
|--------|-------------|------|
| Inversor con [X] desarrollos | `scripts/seed-[nombre-feature].sh --inversor 1 --desarrollos [X]` | |
| | | |

---

## 6. Definición de Done para esta Feature

- [ ] Todos los test cases de prioridad Alta en Pass
- [ ] Todos los TC-SEC-* (aislamiento) en Pass
- [ ] TC-MARCA-* en Pass (copy y tono)
- [ ] Tests de performance dentro de los targets de §4.1
- [ ] Tests de accesibilidad sin violations críticas
- [ ] Sin defectos Blocker ni Major abiertos
- [ ] Sign-off de QA: @_____ — Fecha: ____
- [ ] Sign-off de producto: @_____ — Fecha: ____
- [ ] Sign-off técnico: @_____ — Fecha: ____
- [ ] Sign-off de marca (si hubo copy nuevo): @_____ — Fecha: ____

---

*Siguiente paso: completar `Implementation-Spec.md`*
