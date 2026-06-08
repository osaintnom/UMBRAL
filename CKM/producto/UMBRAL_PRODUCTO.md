# UMBRAL — Qué es este producto

> Documento de bases. Sienta el "qué" y el "para qué" de la plataforma UMBRAL (app del inversor + backoffice) antes de arrancar el diseño mobile-first.
> Fuente de verdad de marca: `../marca/MARCA_UMBRAL.md`. Si algo de acá choca con la marca, gana la marca.
> Última actualización: junio 2026.

---

## 1. La idea central

UMBRAL acompaña al inversor durante el tramo más largo e incierto de su experiencia: **entre la firma y la entrega**. Ese intervalo dura años, y es justo donde el desarrollador se queda en silencio y el inversor queda en el aire.

La plataforma ocupa ese espacio. No con notificaciones vacías ni con un tablero de reclamos — con **presencia, información curada, sentido de pertenencia y una lectura clara del valor que el inversor está construyendo** (cuánto valen hoy sus m², cómo avanza su obra).

La propuesta de valor es para el **desarrollador**: UMBRAL eleva su imagen durante la obra, evita el roce con inversores y convierte a cada inversor en un activo (recompra, referido, prestigio) en lugar de un riesgo. La plataforma es el **soporte** de esa propuesta, no la propuesta en sí.

> Lectura interna honesta: por debajo, el sistema sí carga contenido, manda avisos y gestiona usuarios. Eso es **mecánica**. Lo que se vende y se comunica es **acompañamiento, cercanía y prestigio** — nunca "comunicador", "CRM" ni "postventa" (ver §6).

---

## 2. Los dos productos, un solo backend

```
                ┌───────────────────────────────────────┐
                │          Backend compartido            │
                │  API · Auth · Reglas de negocio · BD   │
                │  Aislamiento por (inversor × desarrollo)│
                └──────────────────┬────────────────────┘
                                   │
                  ┌────────────────┴────────────────┐
                  │                                  │
          ┌───────▼────────┐                ┌────────▼────────┐
          │   App inversor  │                │    Backoffice    │
          │  (mobile-first) │                │ (UMBRAL + desa)  │
          │  consume datos  │                │  carga y opera   │
          └─────────────────┘                └──────────────────┘
```

- **Un backend** sirve a los dos frontends. Lo que carga el backoffice aparece directo en la app, sin duplicar lógica.
- **Dos frontends separados**: app pensada para mobile (inversor), backoffice pensado para desktop (operación).
- **Aislamiento estricto**: cada inversor ve únicamente sus desarrollos. El backend lo enforcea a nivel de permisos, no el front. Esto es requisito de seguridad, no de UI.

---

## 3. La app del inversor (mobile-first)

Es la cara visible. El usuario puede estar en **uno o varios desarrollos** (los wireframes ya muestran "desarrollos +"), y de cada uno ve solo lo suyo.

### 3.1 Acceso y onboarding

- **Onboarding mínimo, una sola vez:** email, y para entrar a un desarrollo → **código de referencia** que lo valida y lo asocia al proyecto + su **inversión en m²**.
- **Login rápido para el día a día:** una vez creada la cuenta, entrar tiene que ser instantáneo. Proponemos **login con Google** (o biométrico en mobile) además de email + contraseña. El campo "código" del wireframe es de *alta a un desarrollo*, no de login recurrente — conviene separar los dos momentos para que el login no pida el código cada vez.
- Un mismo inversor puede sumar más desarrollos cargando otro código de referencia (el "+" del home).

### 3.2 Home del desarrollo

- **Card del desarrollo:** nombre, rango (xxx–yyy), su inversión en m², estado.
- **Proyección de valor por m²** (el bloque verde del wireframe, con la curva +$): es **la joya visual**. Le muestra al inversor cuánto valoriza lo que tiene. Conecta directo con "valorización / línea de salida / % de participación" que la marca define como núcleo de la plataforma del inversor (MARCA §15). Es lo que diferencia a UMBRAL de un comunicador de obra.
- **Contenido curado:** imágenes de obra/proyecto, novedades (news), videos (YouTube embebido o precargados). Honesto con la marca: "tus metros avanzan. Cada etapa se comunica, se registra y se comparte" — sin prometer tiempo real que no existe.
- **FAQ** del desarrollo, accesible inline.

### 3.3 Acciones (barra inferior)

- **Ayuda / Acompañamiento** (botón "soporte" del wireframe): lleva a la vista de contacto y preguntas. *Nota de copy: en la UI evitar la palabra "soporte" — usar "Ayuda", "Acompañamiento" o "Estamos" (MARCA §10 la prohíbe para describir a UMBRAL).*
- **Vender** (el botón rojo del wireframe — reemplaza y mejora el viejo "ABANDONAR PROYECTO"): el inversor que quiere salir abre un **cuestionario breve** (motivo) y dispara un **mail** al equipo. No es una puerta de salida triste: es la **línea de salida** que UMBRAL ofrece. Para el negocio es un arma — detecta intención de venta temprano y le permite al desarrollador gestionar/recolocar el cupo antes de perder al inversor. *"Vender" comunica oportunidad; "abandonar" comunica fuga — quedarse con "Vender" / "Quiero vender mi unidad".*

---

## 4. El backoffice (centro de control)

Lo opera el equipo de UMBRAL y, con permisos acotados, administradores del desarrollador. Regla número uno: **simple, sin fricción, operable por alguien no técnico**. Es el control de **todos** los desarrollos.

**Qué hace en v1:**

- **Habilitar y configurar desarrollos** (alta, datos base, estado de obra).
- **Dar de alta inversores** y generar/administrar los **códigos de referencia** que usan para entrar a su desarrollo. Asociar inversor ↔ desarrollo ↔ m².
- **Cargar el contenido de la app:** imágenes, videos (links/YouTube), novedades, FAQ — por desarrollo.
- **Cargar la proyección de valor por m²** que ve el inversor.
- **Enviar avisos segmentados:** hitos de obra, novedades y **recordatorios de pago**. *Internamente es notificación; hacia el inversor se presenta como acompañamiento, no como cobranza fría.*
- **Ver y gestionar las solicitudes de "Vender"**: bandeja con motivo y datos del inversor para que el equipo actúe.

**Roles (a definir bien, pero v1 necesita al menos):**

- **Admin UMBRAL** — ve y opera todos los desarrollos.
- **Admin desarrollador** — ve solo sus desarrollos (control administrativo, % vendido por unidad, mediciones — MARCA §15).

---

## 5. Modelo de datos mínimo (para arrancar)

- **Usuario/Inversor**: identidad, método de login (email, Google).
- **Desarrollo**: datos base, estado de obra, contenido (imágenes, videos, news, FAQ), curva de valorización por m².
- **Membresía** (inversor × desarrollo): m² invertidos, código de referencia usado, fecha de alta, estado. **Acá vive el aislamiento de permisos.**
- **Solicitud de venta**: inversor, desarrollo, motivo, fecha, estado de gestión.
- **Aviso/Notificación**: tipo (pago / novedad / hito), desarrollo, segmento destino, fecha.

---

## 6. Alineación con la marca (no opcional)

Palabras **prohibidas** en UI y copy externo (MARCA §3, §10): *postventa, CRM, comunicador, atención al cliente, soporte* (como descripción de UMBRAL), *promesa*.

| En el producto se llama… | En la UI / copy decimos… |
| --- | --- |
| Soporte | Ayuda · Acompañamiento · Estamos |
| Notificaciones / recordatorios | Novedades de obra · Avisos · "tus metros avanzan" |
| Abandonar proyecto | **Vender** · "Quiero vender mi unidad" |
| Dashboard de valorización | Tu valor · Proyección de tus m² |

Idioma: **español rioplatense, voseo**. Tono: sobrio, cálido, arquitectónico, frases cortas.

---

## 7. Alcance v1 (qué construimos primero)

Lo mínimo para que el producto **exista y se sienta UMBRAL**:

1. Backend compartido + auth + aislamiento por membresía.
2. App: onboarding con código, login rápido, home de desarrollo (card + valorización + contenido + FAQ), botón Ayuda, botón Vender (cuestionario + mail).
3. Multi-desarrollo (el "+").
4. Backoffice: alta de desarrollos e inversores, códigos de referencia, carga de contenido y valorización, envío de avisos, bandeja de "Vender".

**Fuera de v1 (pero el desa "compra futuro", MARCA §8):** Banca UMBRAL, Cartilla, beneficios, documentos/escrituras, línea de tiempo detallada, comunidad entre inversores. Se nombran como visión, se construyen por madurez.

---

## 8. Decisiones abiertas

- **Login**: ¿Google + email en v1, o solo email primero? (Recomendación: email para alta, Google para reingreso rápido.)
- **Código de referencia**: ¿lo genera el backoffice por inversor (1 código = 1 persona) o por desarrollo (código compartido)? 1×inversor es más seguro y trazable.
- **Validación de m²**: ¿se declara y se aprueba en backoffice, o entra directo? (Sugerido: declara el inversor, confirma UMBRAL.)
- **Recordatorios de pago**: ¿UMBRAL solo avisa, o se integra con el sistema de cobranza del desa? v1 = solo aviso.
- **Roles del desarrollador en backoffice**: ¿read-only o puede cargar contenido? Definir antes de diseñar permisos.

---

## 9. Lo que UMBRAL *no* es (recordatorio)

No es postventa. No es CRM. No es un comunicador. Es un **sistema de acompañamiento** que, durante la obra, eleva la imagen del desarrollador y convierte la experiencia del inversor en recompra y referido. La tecnología es el soporte; el producto es la **compañía, la cercanía y el prestigio**.
