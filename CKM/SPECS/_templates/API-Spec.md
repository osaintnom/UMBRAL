---
title: "API Spec: [nombre de la feature]"
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
tags: [spec, api, contratos]
relacionado: [../../software/README.md]
---

# API / Contract Spec — [Nombre de la Feature]

**Versión de la API:** v[X]
**Technical Spec relacionada:** `Technical-Spec`
**Archivo OpenAPI:** `[ruta]/[nombre-feature].yaml`

> El backend es **compartido** entre la app del inversor y el backoffice. Cada endpoint
> declara qué roles acceden y cómo se enforcea el aislamiento por (inversor × desarrollo).

---

## 1. Convenciones Generales

- **Base URL:** `https://api.umbral.app/v[X]` *(placeholder — ajustar al dominio real)*
- **Autenticación:** Bearer token JWT en header `Authorization`
- **Formato de fechas:** ISO 8601 (`YYYY-MM-DDTHH:mm:ssZ`)
- **Aislamiento:** todo recurso ligado a un desarrollo se filtra por la membresía del usuario autenticado. Un inversor nunca recibe datos de un desarrollo que no es suyo.
- **Paginación:** cursor-based con `next_cursor` y `limit` (máx 100)

---

## 2. Endpoints

> Un bloque por endpoint. Incluir todos los status codes posibles, no solo el 200.

---

### POST /[recurso]

**Propósito:** [Qué crea o qué acción dispara]
**Autenticación:** requerida
**Roles con acceso:** inversor / admin desarrollador / admin UMBRAL

**Request body:**
```json
{
  "campo_obligatorio": "string",
  "campo_opcional": "string | null"
}
```

| Campo | Tipo | Obligatorio | Validación |
|-------|------|-------------|-----------|
| campo_obligatorio | string | sí | max 255 chars |
| campo_opcional | string | no | |

**Respuestas:**

`201 Created`
```json
{ "id": "uuid", "estado": "string", "created_at": "ISO 8601" }
```

`400 Bad Request` — validación de campo fallida
```json
{ "error": "validation_error", "fields": [{ "field": "campo", "message": "..." }] }
```

`401 Unauthorized` — token inválido o expirado
```json
{ "error": "unauthorized", "message": "Token inválido o expirado" }
```

`403 Forbidden` — el usuario no tiene el rol requerido
```json
{ "error": "forbidden", "message": "No tenés permiso para realizar esta acción" }
```

`404 Not Found` — recurso inexistente **o fuera de la membresía del usuario** (no revelar que existe)
```json
{ "error": "not_found", "message": "No encontramos lo que buscás" }
```

`422 Unprocessable Entity` — datos válidos en formato pero inválidos en negocio
```json
{ "error": "business_rule_violation", "code": "[código]", "message": "..." }
```

`500 Internal Server Error`
```json
{ "error": "internal_error", "request_id": "uuid" }
```

---

### GET /[recurso]/:id

**Propósito:**
**Autenticación:** requerida
**Roles con acceso:**

**Path params:**
| Param | Tipo | Descripción |
|-------|------|-------------|
| id | UUID | |

**Respuestas:**

`200 OK`
```json
{ "id": "uuid", "campo": "valor" }
```

`404 Not Found` — inexistente o fuera de la membresía del usuario
```json
{ "error": "not_found", "message": "No encontramos lo que buscás" }
```

---

### GET /[recurso] (lista paginada)

**Propósito:**
**Autenticación:** requerida
**Roles con acceso:**

> La lista se filtra por la membresía del usuario: el inversor solo ve sus desarrollos;
> el admin desarrollador, los suyos; el admin UMBRAL, todos.

**Query params:**
| Param | Tipo | Default | Descripción |
|-------|------|---------|-------------|
| limit | integer | 20 | Máx 100 |
| cursor | string | null | Cursor de la página anterior |

**Respuestas:**

`200 OK`
```json
{ "data": [{ "id": "uuid", "campo": "valor" }], "next_cursor": "string | null", "total": 0 }
```

---

### PATCH /[recurso]/:id

**Propósito:**
**Autenticación:** requerida
**Roles con acceso:**

**Request body:** (solo los campos a actualizar)
```json
{ "campo": "nuevo_valor" }
```

**Respuestas:** `200 OK` · `400` · `403` · `404` · `422`

---

## 3. Catálogo de Errores

> Todos los códigos posibles. El mensaje al usuario nunca expone datos internos
> y respeta el tono de marca (voseo, sobrio).

| Código | HTTP | Descripción técnica | Mensaje al usuario (voseo) | Handling esperado |
|--------|------|--------------------|----------------------------|-------------------|
| `unauthorized` | 401 | Token inválido o expirado | "Tu sesión expiró. Volvé a ingresar." | Redirigir a login |
| `forbidden` | 403 | Sin el rol requerido | "No tenés permiso para esta acción." | Mostrar mensaje, no redirigir |
| `not_found` | 404 | Inexistente o fuera de membresía | "No encontramos lo que buscás." | Mostrar inline |
| `validation_error` | 400 | Campo con formato inválido | Ver campo `fields` | Mostrar errores inline por campo |
| `business_rule_violation` | 422 | Viola regla de negocio | Ver código específico abajo | Mostrar mensaje específico |
| `rate_limit_exceeded` | 429 | Demasiadas requests | "Demasiados intentos. Esperá un momento." | Backoff exponencial |
| `internal_error` | 500 | Error interno — ver `request_id` | "Algo falló de nuestro lado. Intentá de nuevo." | Mensaje genérico + request_id |

### Códigos de error de negocio (422)
| Código | Situación | Mensaje sugerido (voseo) |
|--------|-----------|--------------------------|
| `codigo_referencia_invalido` | El código de alta a un desarrollo no es válido | "Ese código no es válido. Revisalo e intentá de nuevo." |
| | | |

---

## 4. Eventos Asíncronos (si aplica)

> Completar si la feature produce o consume eventos (ej: la solicitud de "Vender" dispara un mail al equipo).

### Eventos que produce esta feature

#### [nombre.del.evento]
**Trigger:** Cuándo se emite
**Destinatario:** servicio / webhook / queue
**Semántica:** at-least-once / at-most-once / exactly-once

**Payload:**
```json
{ "event": "nombre.del.evento", "timestamp": "ISO 8601", "data": { "campo": "valor" } }
```

**Política de retries:** [X] reintentos con backoff exponencial, DLQ en `[nombre-queue]-dlq`

---

## 5. Política de Versionado

- **Versión actual:** v[X]
- **Versiones soportadas simultáneamente:** 2 (actual + anterior)
- **Política de deprecación:** [X] meses de aviso con header `Deprecation`
- **Breaking changes:** requieren nueva versión mayor

---

## 6. Mock Server

- **Herramienta:** Prism / MSW / WireMock
- **Cómo levantarlo:** `[comando]`
- **Cobertura:** happy paths + códigos de error de §3

---

## 7. Criterio de Salida de API Spec

- [ ] Todos los endpoints tienen todos los status codes documentados
- [ ] El archivo OpenAPI valida sin errores
- [ ] Cada endpoint declara roles y cómo se enforcea el aislamiento por membresía
- [ ] El catálogo de errores cubre los casos de negocio de los acceptance criteria
- [ ] Los mensajes de error no exponen datos internos y respetan el tono de marca
- [ ] Mock server levantado para que el frontend integre
- [ ] Revisión aprobada (backend): @_____ — Fecha: ____
- [ ] Revisión aprobada (frontend): @_____ — Fecha: ____

---

*Siguiente paso: completar `Test-Spec.md`*
