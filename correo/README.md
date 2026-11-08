# Herramientas de correo (Gmail)

Skills de Claude Code para estar al día con el correo de pablo@pxsol.com.
Usan el conector de Gmail (y, cuando hace falta, Nexus, Cortex y Calendar).
**Ninguna envía mails ni borra nada**: responder siempre termina en un
borrador que revisás vos, y archivar/marcar leído pide OK antes.

| Comando              | Para qué                                                         | Toca la bandeja |
|----------------------|------------------------------------------------------------------|-----------------|
| `/correo-resumen`    | Resumen de las últimas 24 h (o el período que digas).            | No              |
| `/correo-bandeja`    | Triage de lo no leído: Responder / Alerta / Agenda / Info / Ruido, y orden con un OK. | Sí, con OK |
| `/correo-pendientes` | Lo que debo responder y lo que mandé sin respuesta.               | Etiquetas, con OK |
| `/correo-responder`  | Redacta respuestas con tu tono y las deja como borrador en Gmail. | Sólo borradores |
| `/correo-limpiar`    | Saca de encima el backlog grande, agrupando por remitente.        | Sí, con OK por grupo |

## Rutina sugerida

1. **Una sola vez**: `/correo-limpiar` para el backlog de más de 7 días.
2. **Cada mañana**: `/correo-resumen` (o como tarea programada).
3. **1-2 veces por día**: `/correo-bandeja` → `/correo-responder 1 2 …`.
4. **Viernes**: `/correo-pendientes` para no dejar nada colgado.

## Cómo se adapta

Todo el criterio vive en [`reglas.md`](reglas.md): categorías, remitentes,
tono de las respuestas y qué se puede hacer automáticamente. Cuando corrijas
una clasificación, la skill te propone sumar la regla ahí.

## Dónde funcionan

- **Claude Code** abierto en este repo: las skills están en `.claude/skills/`.
- **claude.ai**: se pueden subir como skills de tu cuenta (cada carpeta de
  `.claude/skills/correo-*` es una skill); en ese caso copiá el contenido de
  `reglas.md` dentro de cada una o subilo aparte, porque allá no existe el repo.

## Etiquetas de Gmail que crean

`Claude/Responder`, `Claude/Esperando`, `Claude/Revisar` (se crean la primera
vez, con tu OK).
