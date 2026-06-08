---
title: "Design Spec: [nombre de la feature]"
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
tags: [spec, design, ux]
relacionado: [../../marca/MARCA_UMBRAL.md]
---

# Design Spec — [Nombre de la Feature]

**Versión:** 1.0
**PRD relacionado:** `PRD-Spec`
**Figma / link al diseño:** [URL]
**Aplica a:** ⬜ App del inversor (mobile-first) · ⬜ Backoffice (desktop)

> **Marca primero.** Toda decisión visual se deriva de `MARCA_UMBRAL.md` §11 (paleta, tipografía, logo, estilo). El Copy Deck (§5) se revisa contra la marca antes del Gate 1.

---

## 1. Inventario de Estados

> Todo lo que puede aparecer en pantalla debe estar diseñado antes del build.

### Happy paths
| ID | Flujo | Pantalla(s) involucrada(s) |
|----|-------|--------------------------|
| HP-01 | | |
| HP-02 | | |

### Estados de error
| ID | Error | Trigger | Pantalla donde aparece |
|----|-------|---------|----------------------|
| ERR-01 | Fallo de conexión | API no responde en > 5s | |
| ERR-02 | Sesión expirada | Token inválido o vencido | |
| ERR-03 | Permiso denegado | Inversor sin acceso a ese desarrollo | |
| ERR-04 | | | |

### Estados de carga
| ID | Acción | Tipo de loading |
|----|--------|----------------|
| LOAD-01 | Carga inicial de datos | Skeleton screen |
| LOAD-02 | Acción del usuario (submit, confirm) | Spinner inline / botón deshabilitado |
| LOAD-03 | | |

### Estados vacíos
| ID | Cuándo aparece | Mensaje y acción sugerida |
|----|---------------|--------------------------|
| EMPTY-01 | Inversor sin desarrollos todavía (antes de cargar su primer código) | |
| EMPTY-02 | Desarrollo sin contenido cargado aún | |
| EMPTY-03 | | |

### Estados de permiso / aislamiento
| ID | Segmento sin acceso | Qué ve |
|----|---------------------|--------|
| PERM-01 | Inversor intenta ver un desarrollo que no es suyo | |
| PERM-02 | Admin desarrollador intenta ver un desarrollo de otro | |
| PERM-03 | | |

---

## 2. Wireframes

> Links a Figma o imágenes embebidas. Un wireframe por estado relevante del inventario.

### HP-01 — [Nombre del flujo]
[Link a frame en Figma o imagen]

**Anotaciones:**
- Componente X hace Y cuando el usuario hace Z
- Si el campo está vacío, el botón de submit permanece deshabilitado

### ERR-01 — Fallo de conexión
[Link a frame en Figma o imagen]

**Anotaciones:**
- Mostrar aviso no intrusivo con opción de reintentar
- No bloquear la pantalla completa

*(Repetir por cada estado relevante)*

---

## 3. Mockups de Alta Fidelidad

**Figma — link al proyecto:** [URL]
**Versión del design system usada:** [ref a `diseño.sistema.*`]

### Breakpoints cubiertos
- [ ] Mobile (375px) — prioritario en la app del inversor
- [ ] Tablet (768px)
- [ ] Desktop (1280px) — prioritario en el backoffice

### Estados diseñados en alta fidelidad
- [ ] HP-01 — [nombre] — [link al frame]
- [ ] HP-02 — [nombre] — [link al frame]
- [ ] ERR-01 — [nombre] — [link al frame]
- [ ] LOAD-01 — [nombre] — [link al frame]
- [ ] EMPTY-01 — [nombre] — [link al frame]
- [ ] PERM-01 — [nombre] — [link al frame]

---

## 4. Interaction Spec

### Transiciones y animaciones
| Elemento | Tipo de transición | Duración | Easing |
|----------|-------------------|----------|--------|
| Modal de confirmación | Fade in + scale | 200ms | ease-out |
| Aviso / toast | Slide desde arriba | 250ms | ease-in-out |
| | | | |

### Comportamiento de formularios

**Validación:**
- [ ] En tiempo real (onChange) para campos críticos (ej: email, código de referencia)
- [ ] Al submit para el resto
- [ ] Inline bajo cada campo (no modal)

**Mensajes de error por campo:**
| Campo | Error | Mensaje (voseo) |
|-------|-------|-----------------|
| Email | Formato inválido | "Ingresá un email válido" |
| Código de referencia | Inválido / no encontrado | "Ese código no es válido. Revisalo e intentá de nuevo." |
| | | |

### Feedback de acciones
| Acción | Feedback | Duración visible |
|--------|----------|-----------------|
| Guardado exitoso | Aviso "Listo, se guardó" | 3s |
| Error de red | Aviso + botón reintentar | Hasta que se cierra |
| Solicitud de "Vender" enviada | Confirmación + mail al equipo | — |

### Navegación y gestos
- [ ] El back del navegador/dispositivo funciona en todos los flujos
- [ ] Sin trampas de teclado (foco sale de modales con Escape)
- [ ] Gestos en mobile si aplica: describir

---

## 5. Copy Deck

> Todo el texto visible debe estar acá antes del build.
> **Revisión de marca obligatoria:** voseo rioplatense, tono sobrio/arquitectónico, sin palabras prohibidas (postventa, CRM, comunicador, soporte, atención al cliente, promesa). Usar el vocabulario de reemplazo (`MARCA_UMBRAL.md` §10, `UMBRAL_PRODUCTO.md` §6).

### Títulos y headlines
| Pantalla / componente | Copy |
|----------------------|------|
| | |

### Labels de formulario
| Campo | Label | Placeholder | Tooltip |
|-------|-------|-------------|---------|
| | | | |

### Mensajes de error
| Código | Mensaje para el usuario (voseo) | Nota interna |
|--------|--------------------------------|--------------|
| ERR-01 | "No pudimos conectarnos. Revisá tu conexión e intentá de nuevo." | |
| ERR-02 | "Tu sesión expiró. Volvé a ingresar." | |
| ERR-03 | "No tenés acceso a este desarrollo." | |

### Textos de estados vacíos
| Estado | Título | Subtítulo | CTA |
|--------|--------|-----------|-----|
| EMPTY-01 | | | |
| EMPTY-02 | | | |

### Avisos y notificaciones que dispara esta feature
| Trigger | Destinatario | Asunto / título | Resumen |
|---------|-------------|-----------------|---------|
| | inversor / equipo UMBRAL / admin desa | | |

> Internamente puede ser "notificación"; hacia el inversor se presenta como **acompañamiento / novedad de obra**, nunca como cobranza fría (`UMBRAL_PRODUCTO.md` §4, §6).

### Checklist de marca del Copy Deck
- [ ] Todo en voseo rioplatense
- [ ] Sin palabras prohibidas
- [ ] Sin promesas de tech inexistente
- [ ] Revisado por el guardián de marca: @_____ — Fecha: ____

---

## 6. Component Inventory

### Componentes existentes que se reutilizan
| Componente | Variante | Link al design system (`diseño.sistema.componentes`) |
|------------|----------|------|
| | | |

### Componentes nuevos a crear
| Componente | Descripción | Reutilizable en otras features |
|------------|-------------|-------------------------------|
| | | sí / no |

---

## 7. Criterio de Salida de Design Spec

- [ ] Todos los estados del inventario (§1) tienen diseño aprobado
- [ ] Breakpoints relevantes cubiertos (mobile para app, desktop para backoffice)
- [ ] Interaction spec completa para formularios y transiciones
- [ ] Copy Deck completo y **revisado contra la marca** (voseo, palabras prohibidas, honestidad)
- [ ] Estados de aislamiento (PERM-*) diseñados
- [ ] Component inventory distingue qué se construye vs qué ya existe
- [ ] Implementabilidad confirmada por quien va a construir
- [ ] Sign-off de producto: @_____ — Fecha: ____
- [ ] Sign-off de marca: @_____ — Fecha: ____

---

*Siguiente paso: completar `Technical-Spec.md`*
