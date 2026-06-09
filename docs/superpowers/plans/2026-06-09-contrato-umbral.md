# UMBRAL MVP Contract Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Producir un contrato formal, breve y editable para el desarrollo del MVP de UMBRAL, con anexos de alcance y condiciones comerciales.

**Architecture:** El contrato tendrá un cuerpo principal para las reglas generales, un Anexo A que congela el alcance funcional vigente y un Anexo B con precio, plazo, pagos y mantenimiento. El DOCX utilizará un estilo empresarial sobrio, tablas solo para datos comparables y una copia PDF derivada del mismo archivo.

**Tech Stack:** Python bundled runtime, `python-docx`, LibreOffice headless y el renderer de la skill Documents.

---

### Task 1: Redactar el contenido contractual

**Files:**
- Create: `/private/tmp/umbral_contract/UMBRAL_contrato_desarrollo_MVP_v01_2026-06-09.docx`

- [ ] **Step 1: Consolidar el alcance**

Usar `CKM/producto/MVP.md` y `CKM/SPECS/mvp-v1/PRD-Spec.md` como fuentes del
alcance. Excluir el acceso de desarrolladoras, multi-desarrollo, cobranza
integrada y módulos futuros.

- [ ] **Step 2: Redactar las cláusulas generales**

Incluir objeto, jerarquía documental, entregas, demo, revisiones, plazo, precio,
responsabilidades, datos, propiedad intelectual, confidencialidad, restricción
competitiva, garantía, mantenimiento, responsabilidad, terminación y
comunicaciones.

- [ ] **Step 3: Redactar los anexos**

El Anexo A debe enumerar funcionalidades y exclusiones. El Anexo B debe incluir
las dos opciones de pago para seleccionar, plazo, cotización MEP, costos
externos y mantenimiento.

### Task 2: Construir y auditar el DOCX

**Files:**
- Create: `/private/tmp/umbral_contract/build_contract.py`
- Create: `/private/tmp/umbral_contract/UMBRAL_contrato_desarrollo_MVP_v01_2026-06-09.docx`

- [ ] **Step 1: Aplicar el preset**

Usar `standard_business_brief`, página Letter, márgenes de 1 pulgada, cuerpo
Calibri 11, jerarquía sobria y tablas de geometría fija.

- [ ] **Step 2: Ejecutar auditoría estructural**

Verificar títulos, numeración, tablas, campos pendientes, cláusulas
contradictorias y ausencia de contenido técnico innecesario.

### Task 3: Renderizar, revisar y entregar

**Files:**
- Create: `/private/tmp/umbral_contract/render/`
- Create: `/Users/olisaintnom/Downloads/Proyectos/UMBRAL_contrato_desarrollo_MVP_v01_2026-06-09.docx`
- Create: `/Users/olisaintnom/Downloads/Proyectos/UMBRAL_contrato_desarrollo_MVP_v01_2026-06-09.pdf`

- [ ] **Step 1: Renderizar DOCX a PNG y PDF**

Ejecutar `render_docx.py` con `--emit_pdf` y comprobar que existe una imagen por
página.

- [ ] **Step 2: Inspeccionar todas las páginas**

Comprobar que no haya texto cortado, tablas desbordadas, saltos de página
defectuosos, inconsistencias de fuente ni campos ilegibles.

- [ ] **Step 3: Copiar los archivos finales**

Copiar únicamente el DOCX y PDF finales a `/Users/olisaintnom/Downloads/Proyectos`.

