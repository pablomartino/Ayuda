---
name: correo-resumen
description: Resumen ejecutivo del correo de Gmail de Pablo para un período (default últimas 24 h) - lo que pasó, lo que importa, lo que hay que hacer - sin tocar la bandeja. Pensado para leer rápido a la mañana o para correr como tarea programada. Usar con "/correo-resumen", "resumime el mail de hoy", "qué pasó en el correo mientras no estaba", "resumen del mail de la semana".
---

# Resumen del correo

Sólo lectura: no archiva, no marca, no etiqueta. Para ordenar la bandeja está
`/correo-bandeja`.

## Argumentos opcionales

- Período: `hoy`, `24h` (default), `fin de semana`, `semana`, `desde <fecha>`.
- `con leídos`: incluir también lo ya leído (default: todo lo recibido en el
  período, leído o no, excluyendo Promociones).

## Pasos

1. Leer `correo/reglas.md`.
2. `mcp__Gmail__search_threads`: `in:inbox newer_than:1d -category:promotions`
   (ajustar período), `THREAD_VIEW_SUMMARY`, paginando.
3. Clasificar con las reglas. Leer con `get_thread` (`PLAIN_TEXT`) sólo los
   hilos humanos y las alertas, para resumirlos bien.
4. Agrupar notificaciones repetidas en una línea con números
   ("CES: 5 positivos, 1 neutro (Hotel X)", "FQ: 3 en seguimiento, 1 cerrado").
5. Revisar también `in:sent` del período para detectar compromisos que Pablo
   asumió ("te lo mando el lunes") y listarlos como pendientes propios.

## Salida (máximo ~25 líneas)

```
☀️ Correo — <período> · <N> hilos

Lo importante
- <1-5 bullets: lo que Pablo no puede dejar de saber, con link>

Para hacer
- [ ] Responder a <quién> sobre <qué>
- [ ] <compromiso propio detectado en enviados>

Alertas del sistema
- P0: … · NPS bajo: … · FQ nuevos: …

Agenda que llegó por mail
- <día hora> <reunión>

Resto
- <n> informativos, <n> ruido (no se tocaron)
```

Cerrar ofreciendo `/correo-bandeja` para ordenar o `/correo-responder` para
los "Para hacer".

## Como tarea programada

Si Pablo pide recibirlo todos los días, crear una tarea programada
(`create_trigger` con `create_new_session_on_fire: true`, días hábiles, en su
zona horaria America/Argentina/Buenos_Aires, antes de las 9) cuyo prompt sea
"Corré /correo-resumen de las últimas 24 h (lunes: desde el viernes)".
Pedir confirmación del horario antes de crearla.
