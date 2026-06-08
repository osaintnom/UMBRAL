---
title: "Discovery: [nombre de la feature]"
area: specs
audiencia: interno
tipo: template
sensibilidad: interno
owner: "@"
estado: borrador
revision-cada: "30d"
ultima-revision: ""
feature-status: backlog
tags: [spec, discovery]
relacionado: []
---

# Discovery — [Nombre de la Feature]

> **Cómo usar este template**
> Completá cada sección antes de hablar de soluciones o de diseño.
> Si alguna sección no puede completarse con evidencia real, es señal de que falta investigación.
> Eliminá este bloque antes de subir al repo.

**Aplica a:** ⬜ App del inversor (mobile) · ⬜ Backoffice (desktop) · ⬜ Backend

---

## 1. Problem Statement

> Describí el problema sin mencionar ninguna solución, tecnología ni componente de UI.
> Si el texto menciona botones, pantallas, endpoints o servicios, lo estás haciendo mal.

**¿Quién tiene el problema?**
<!-- Ej: el inversor durante los años entre la firma y la entrega / el desarrollador que pierde imagen durante la obra / el equipo UMBRAL que opera el backoffice -->

**¿Cuál es la situación actual?**
<!-- Qué pasa hoy, qué hace la persona, qué fricción encuentra -->

**¿Cuál es el impacto de no resolverlo?**
<!-- Para el inversor / para el desarrollador (su imagen, recompra, referido) / para UMBRAL -->

**¿Qué evidencia tenemos de que este problema es real?**
<!-- Conversaciones con desarrolladoras, comportamiento del inversor, wireframes, MARCA_UMBRAL.md, analítica -->
- Fuente 1:
- Fuente 2:
- Fuente 3:

---

## 2. Stakeholders y Restricciones

### Stakeholders

| Rol | Nombre | Tipo de involucramiento | Nivel de influencia |
|-----|--------|------------------------|---------------------|
| Responsable de producto | | Responsable / aprueba | Alta |
| Quien implementa (tech) | | Revisa / aprueba técnico | Alta |
| Guardián de marca | | Valida copy y posicionamiento contra `MARCA_UMBRAL.md` | Alta |
| Desarrollador (cliente B2B) | | Validar valor para su negocio | Media |
| Inversor representativo | | Validar problema y solución | Media |

### Restricciones Técnicas
<!-- Backend compartido, dos frontends separados, sistemas de terceros que no cambian -->
- [ ]
- [ ]

### Restricciones de Negocio
<!-- Deadline, presupuesto, alcance v1, qué es "comprar futuro" (MARCA §8) -->
- [ ]
- [ ]

### Alineación de Marca (obligatorio en UMBRAL)
<!-- ¿La feature introduce copy, nombres o conceptos visibles al usuario? -->
- [ ] Introduce copy/UI visible → revisar palabras prohibidas y tono (`MARCA_UMBRAL.md` §3, §10)
- [ ] Nombra una acción o vista → validar contra el vocabulario de reemplazo (`UMBRAL_PRODUCTO.md` §6)
- [ ] Promete comportamiento (ej: "tiempo real") → confirmar que es honesto y existe
- [ ] No introduce nada visible al usuario (interno / backoffice operativo)

### Aislamiento de datos (obligatorio en UMBRAL)
- [ ] Toca datos del inversor → la solución debe respetar el aislamiento por (inversor × desarrollo)
- [ ] Toca el backoffice → definir qué ve Admin UMBRAL vs Admin desarrollador
- [ ] No toca datos sensibles

### Dependencias
| Dependencia | Estado | Responsable |
|-------------|--------|-------------|
| | | |

---

## 3. Usuarios y Jobs-to-be-Done

### Segmentos afectados
- [ ] Inversor (usuario final de la app, mobile-first)
- [ ] Desarrollador (cliente B2B que paga)
- [ ] Admin desarrollador (opera su desarrollo en el backoffice)
- [ ] Equipo UMBRAL (opera todo el backoffice)
- [ ] Otro: ___________

### Jobs-to-be-Done
> Formato: "Cuando [situación], quiero [motivación], para [resultado esperado]"

**Inversor**
- Cuando _____, quiero _____, para _____.
- Cuando _____, quiero _____, para _____.

**Desarrollador / Admin desarrollador**
- Cuando _____, quiero _____, para _____.

**Equipo UMBRAL**
- Cuando _____, quiero _____, para _____.

---

## 4. Métricas de Éxito

### Métrica primaria
| Métrica | Estado actual | Target | Timeframe | Cómo se mide |
|---------|--------------|--------|-----------|--------------|
| | | | | |

### Métricas secundarias
| Métrica | Dirección esperada | Cómo se mide |
|---------|-------------------|--------------|
| | | |

### Métricas de guardrail
> No deben empeorar con el lanzamiento.

| Métrica | Umbral mínimo aceptable |
|---------|------------------------|
| | |

---

## 5. Criterio de Salida de Discovery

- [ ] Problem statement escrito sin mencionar soluciones y acordado por producto y stakeholders
- [ ] Al menos una fuente de evidencia primaria documenta el problema
- [ ] Stakeholders mapeados con nivel de involucramiento
- [ ] Restricciones técnicas y de negocio documentadas
- [ ] Alineación de marca evaluada (palabras prohibidas, tono, honestidad)
- [ ] Aislamiento de datos evaluado si la feature toca datos del inversor
- [ ] Métricas de éxito definidas con targets y forma de medición
- [ ] Dependencias identificadas con estado

---

*Siguiente paso: completar `PRD-Spec.md`*
