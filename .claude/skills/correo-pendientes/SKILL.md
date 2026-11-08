---
name: correo-pendientes
description: Lista lo que Pablo tiene pendiente en Gmail en las dos direcciones - correos donde alguien espera su respuesta (incluso ya leídos) y correos que él mandó y no le contestaron. Ordena por antigüedad, y ofrece redactar respuestas o recordatorios. Usar con "/correo-pendientes", "qué mails debo", "a quién no le contesté", "qué mails mandé sin respuesta", "seguimientos de correo".
---

# Pendientes de correo

La bandeja "no leídos" engaña: muchas cosas se leen y quedan sin responder.
Esta skill busca la deuda real.

## Argumentos opcionales

- `debo`: sólo lo que yo tengo que responder.
- `esperando`: sólo lo que mandé y no me respondieron.
- Período: default 14 días (`newer_than:14d`).

## A) Lo que debo responder

1. Buscar con `mcp__Gmail__search_threads` (`THREAD_VIEW_SUMMARY`, `pageSize: 50`):
   `in:inbox newer_than:14d -category:promotions -from:me to:pablo@pxsol.com`
   más los hilos con la etiqueta `label:Claude-Responder` (sin límite de fecha).
2. Descartar remitentes automáticos según `correo/reglas.md`
   (no-reply, notificaciones@, mailer-daemon, newsletters, invitaciones).
3. Para cada candidato, `mcp__Gmail__get_thread` (`PLAIN_TEXT`) y quedarse con
   los hilos cuyo **último mensaje no es de pablo@pxsol.com** y que contienen
   una pregunta, pedido o próximo paso para Pablo.
4. Ordenar: primero clientes/partners externos, después tickets `[NX#…]`,
   después internos; dentro de cada grupo, el más viejo primero.

## B) Lo que estoy esperando

1. Buscar `in:sent newer_than:14d` (y `label:Claude-Esperando`).
2. Para cada hilo, `get_thread` en `METADATA_ONLY` primero: si el último mensaje
   es de Pablo y tiene más de 2 días hábiles, es candidato.
3. Leer en `PLAIN_TEXT` sólo los candidatos para confirmar que el mail pedía
   algo (una pregunta, una confirmación, un dato). Un "gracias" o un FYI no
   genera seguimiento.

## Salida

```
⏳ Pendientes de correo — últimos 14 días

Debo responder (n)
1. <Remitente> — <asunto> · hace <x> días
   → <qué espera de mí>  [abrir](viewUrl)

Estoy esperando (n)
7. <Destinatario> — <asunto> · mandado hace <x> días
   → <qué pedí>  [abrir](viewUrl)
```

## Después

- Ofrecer con `AskUserQuestion` (multiSelect) qué hacer:
  - Etiquetar los de A con `Claude/Responder` y los de B con `Claude/Esperando`
    (crear las etiquetas si faltan).
  - Redactar respuestas con `/correo-responder <números>`.
  - Redactar recordatorios amables para los de B como **borradores** (nunca
    enviar): `mcp__Gmail__create_draft` con `replyToMessageId` del último
    mensaje, tono según `correo/reglas.md`.
- Quitar la etiqueta `Claude/Responder` / `Claude/Esperando` de los hilos que
  ya se resolvieron (el último mensaje cambió de lado), avisando cuáles.

## Límites

Nunca enviar. Sólo borradores, y siempre mostrando el texto antes de crearlos.
