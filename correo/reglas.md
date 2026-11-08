# Reglas de clasificación del correo

Este archivo lo leen todas las skills `correo-*`. Editalo cuando quieras cambiar
cómo se clasifica algo: es la "memoria" del sistema. Las skills pueden proponerte
agregar reglas nuevas (por ejemplo "archivar siempre lo de X"), pero sólo lo
escriben acá con tu OK.

## Quién soy

- Pablo Martino — pablo@pxsol.com — Pxsol (vertical PMS).
- Mis respuestas: español rioplatense (vos), cordial y directo, sin vueltas.
  Firmo "Pablo". Con clientes, un poco más formal; con el equipo, informal.

## Categorías

Cada hilo cae en UNA categoría (la primera que aplique, en este orden):

### 1. 🔴 Responder — alguien espera algo de mí
- Remitente humano (no `no-reply`, `notificaciones@`, `mailer-daemon`, newsletters)
  y yo estoy en **Para** (no sólo en CC), o me nombran / me preguntan algo directo.
- Tickets `[NX#…]` donde el último mensaje es de un cliente o colega y me pide algo.
- `Recordatorio: ticket #… sigue esperando tu respuesta`.
- Minutas de reunión con clientes o partners que tienen próximos pasos para mí.

### 2. 🟠 Alerta — mirar hoy aunque no haya que responder
- Asuntos que empiezan con `P0` (incluye `P0 fiscal`).
- `NPS 0`, `NPS 1`… `NPS 6` — "necesita una llamada".
- `FQ-xx · Nombre…` **nuevo** (formulario de queja abierto) u `observación de Calidad`.
- `Pregunta nueva en la ficha de PMS` (→ sugerir `/preguntaspms`).
- `autorización para …` (algo espera mi aprobación).
- Incidentes de seguridad de proveedores que uso (ej. Xubio).
- `Delivery Status Notification (Failure)` de un mail que mandé yo.

### 3. 📅 Agenda
- Invitaciones de calendario (`Invitación:`, `Invitación actualizada:`, `Nueva reunión reservada`).
- Se informan agrupadas; no se responden desde acá.

### 4. 🟢 Informativo — está bien saberlo, no requiere acción
- `CES TK-…: … (Positivo)`.
- `FQ-xx sigue abierto, en seguimiento`, `FQ-xx cerrado`, `FQ-xx · nueva actualización / evidencia`.
- `Egreso ONB: …`, `Trial creado: …`.
- `[Mejoras] Votá: …`.
- Hilos internos donde estoy en CC y nadie me pregunta nada.
- Informes automáticos (tl;dv, Google Business Profile, reportes de rendimiento).

### 5. ⚪ Ruido — se puede archivar
- Categoría Promociones de Gmail.
- Newsletters y marketing (`news.`, `email.openai.com`, `productdirection.co`,
  `ocasa.com` salvo que sea un envío mío, etc.).
- `Tus productos no están públicos` y similares de plataformas.

> CES **negativo o neutro** NO es informativo: va a 🟠 Alerta.

## Etiquetas de Gmail que usa el sistema

Se crean la primera vez que hagan falta (con tu OK):

| Etiqueta            | Para qué                                            |
|---------------------|-----------------------------------------------------|
| `Claude/Responder`  | Hilos donde debo una respuesta.                     |
| `Claude/Esperando`  | Mandé algo y espero respuesta del otro lado.        |
| `Claude/Revisar`    | Alertas para mirar con tiempo.                      |

## Acciones automáticas permitidas (con un único OK por lote)

- Archivar (= quitar `INBOX`) los hilos ⚪ Ruido.
- Marcar como leídos (= quitar `UNREAD`) los 🟢 Informativos.
- Nunca: borrar, mandar a spam, enviar mails o responder invitaciones sin OK explícito
  por cada uno.

## Remitentes conocidos

Agregá acá excepciones puntuales (remitente → categoría):

- `claudio@pxsol.com` con "Recordatorio: ticket" → 🔴 Responder
- `notificaciones@pxsol.com` → según asunto (ver arriba); por defecto 🟢 Informativo
- `no-reply@pxsol.com` → según asunto (ver arriba); por defecto 🟢 Informativo
