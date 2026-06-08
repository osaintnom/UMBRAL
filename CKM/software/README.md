---
title: "Software — índice"
area: software
audiencia: interno
tipo: referencia
sensibilidad: interno
owner: "@santiromero1"
estado: borrador
revision-cada: "180d"
ultima-revision: "2026-06-08"
tags: [software, indice, arquitectura]
relacionado: [../producto/UMBRAL_PRODUCTO.md]
---

# software/

Conocimiento técnico transversal de UMBRAL: arquitectura, modelo de datos, integraciones, deploy, seguridad. Es el contexto estable que las Technical Specs de cada feature referencian (en lugar de repetirlo).

**Todavía vacío.** Se llena al definir la arquitectura, antes del Gate 2 de la primera feature. Convención: `software.subtema.nombre.md`.

Documentos esperables:

| Documento | Qué contendrá |
|---|---|
| `software.arquitectura.overview.md` | Visión general: backend compartido + dos frontends (app mobile / backoffice desktop), stack. |
| `software.arquitectura.modelo-datos.md` | Schema: Inversor, Desarrollo, Membresía, Solicitud de venta, Aviso. **Aislamiento por (inversor × desarrollo).** |
| `software.seguridad.aislamiento.md` | Cómo el backend enforcea que cada inversor vea solo sus desarrollos. |
| `software.deploy.produccion.md` | Proceso de deploy y rollback. |
