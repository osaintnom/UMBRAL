---
title: "Release: [nombre de la feature]"
area: specs
audiencia: interno
tipo: proceso
sensibilidad: interno
owner: "@"
estado: borrador
revision-cada: "30d"
ultima-revision: ""
feature-status: completado
pr-relacionado: ""
tags: [spec, release, runbook]
relacionado: [../../software/README.md]
---

# Release y Evolución — [Nombre de la Feature]

**Validation Report:** `Validation-Spec`
**Fecha de deploy:** ____
**Versión:** [tag de release]
**Aplica a:** ⬜ App del inversor · ⬜ Backoffice · ⬜ Backend

---

## 1. Estrategia de Deploy

### Estrategia elegida
- [ ] **Feature flag** — activar para X% de usuarios, incrementar gradualmente
- [ ] **Canary deployment** — X% del tráfico al nuevo código
- [ ] **Lanzamiento completo** — riesgo bajo y validación exhaustiva

**Justificación:**

### Plan de rollout (feature flag o canary)
| Fase | Porcentaje | Duración | Métricas a monitorear antes de continuar |
|------|-----------|----------|------------------------------------------|
| 1 | 5% | 24hs | Sin errores 5xx. Métrica primaria estable. |
| 2 | 25% | 24hs | |
| 3 | 100% | — | |

---

## 2. Umbral de Rollback

> Definir antes del deploy qué condición dispara rollback inmediato (sin aprobación).

| Métrica | Umbral de rollback automático |
|---------|------------------------------|
| Tasa de error 5xx | > [X]% del tráfico en 15 minutos |
| Latencia P95 | > [X]ms sostenida por 10 minutos |
| [Métrica de guardrail específica] | degradación > [X]% |
| **Fuga de aislamiento** (un inversor ve datos de otro desarrollo) | cualquier ocurrencia |

**Procedimiento de rollback:** ver `software.deploy.produccion` / `software.deploy.rollback`.

---

## 3. Runbook Operacional

> Para el equipo de on-call. Comprensible sin contexto previo de la feature.

### 3.1 Métricas a monitorear

| Métrica | Dashboard | Umbral de alerta | Umbral crítico |
|---------|-----------|-----------------|----------------|
| Tasa de error de `POST /[recurso]` | [link] | > 1% | > 3% |
| Latencia P95 de `GET /[recurso]` | [link] | > 400ms | > 800ms |
| [Métrica de negocio] | [link] | | |
| Errores de aislamiento / datos de inversor | [link] | cualquier ocurrencia | — |

### 3.2 Diagnóstico de problemas frecuentes

#### Problema: Alta tasa de errores en `[endpoint]`
**Posibles causas:**
1.
2.

**Cómo diagnosticar:**
```bash
# Ver últimos errores con request_id
# [comando de logs]
```

**Acción:**
- Si es por [causa 1]: [acción]
- Si es por [causa 2]: escalar a [persona/equipo]

---

#### Problema: Sospecha de fuga de aislamiento (un inversor ve datos de otro)
> **Prioridad máxima.**

**Acción inmediata:**
1. Ejecutar rollback (es condición de rollback automático — §2).
2. Notificar a @tech y @producto en menos de 15 minutos.
3. Auditar logs para determinar alcance.

---

### 3.3 Escalamiento

| Severidad | Quién contactar | Canal | SLA |
|-----------|----------------|-------|-----|
| Crítica (fuga de datos, sistema caído) | @tech + @producto | Canal de incidentes + llamada | Inmediato |
| Alta (tasa de error > umbral) | @tech | Canal de alertas | 30 min |
| Media (latencia elevada) | On-call | Canal de alertas | 2 hs |

---

## 4. Release Notes

> Para comunicar al equipo y, si aplica, a desarrolladores. Sin jerga técnica, en tono de marca (voseo, sobrio).

**Título:** [Nombre legible de la feature]
**Fecha:** ____
**Audiencia:** inversor / desarrollador / equipo interno

**Qué hay de nuevo:**
[Qué puede hacer el usuario ahora que antes no podía]

**Cómo usarlo:**
[Instrucciones breves si aplica]

**Preguntas frecuentes:**
- **¿Afecta mis desarrollos existentes?** [Respuesta]
- **¿Necesito hacer algo?** [Respuesta]

> Revisar que el copy de las release notes hacia el inversor respete la marca: nada de "soporte", "postventa" ni "comunicador" — es acompañamiento.

---

## 5. Documentación Viva

### Docs a actualizar post-lanzamiento

| Documento | Cambio necesario | Estado | Responsable |
|-----------|-----------------|--------|-------------|
| `software.arquitectura.overview` | Agregar nuevo componente/servicio | | |
| `software.arquitectura.modelo-datos` | Actualizar schema | | |
| `producto/UMBRAL_PRODUCTO.md` | Actualizar alcance si cambió | | |
| `../README.md` (memoria del proyecto) | Actualizar §7 con el estado | | |

### Actualización de frontmatter
Todos los docs de spec de esta feature pasan a:
```yaml
feature-status: completado
estado: vigente
ultima-revision: "[fecha de lanzamiento]"
```

---

## 6. Monitoreo Post-lanzamiento

### Semana 1
| Día | Métrica primaria | Métricas de guardrail | Observaciones |
|-----|-----------------|----------------------|--------------|
| Día 1 | | | |
| Día 3 | | | |
| Día 7 | | | |

### Evaluación a 30 días
- **Métrica primaria:** [resultado] vs. target [target]
- **¿Se alcanzó el criterio de éxito del Discovery?** Sí / No / Parcialmente
- **Aprendizajes para el roadmap:**

---

## 7. Retrospectiva del Proceso

> Foco en el proceso, no en el resultado.

**¿Qué fase tomó más tiempo del estimado?**

**¿Hubo spec amendments significativos? ¿Qué los causó?**

**¿Qué spec estaba incompleta y generó re-trabajo?**

**¿Algo funcionó especialmente bien?**

**Tres acciones para el próximo ciclo:**
1.
2.
3.

---

## 8. Criterio de Cierre de la Feature

- [ ] Feature en producción dentro de los parámetros del umbral de rollback
- [ ] Métricas de guardrail sin regresiones después de 48hs
- [ ] Sin fugas de aislamiento detectadas
- [ ] Runbook presentado al equipo de on-call
- [ ] Release notes comunicadas
- [ ] Todos los docs de spec actualizados (feature-status: completado)
- [ ] Docs de arquitectura actualizados si hubo cambios estructurales
- [ ] Memoria del proyecto (`../README.md` §7) actualizada
- [ ] Retrospectiva completada

---

*Esta feature está cerrada. Cualquier cambio futuro empieza en un nuevo `PRD-Spec`.*
