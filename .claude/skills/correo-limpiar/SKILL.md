---
name: correo-limpiar
description: Limpieza masiva del backlog de Gmail (cientos de no leídos). Agrupa los correos por remitente y tipo, muestra cuántos hay de cada grupo y, con un OK por grupo, los archiva o los marca como leídos, dejando a la vista sólo lo que puede necesitar respuesta. Usar con "/correo-limpiar", "limpiá mi bandeja", "tengo 800 mails sin leer", "inbox zero", "declarar bancarrota de mail".
---

# Limpieza del backlog

Para salir de un pozo de cientos de no leídos sin revisarlos uno por uno.
Nada se borra: archivar sólo saca de la bandeja (se sigue encontrando con la
búsqueda y en "Todos").

## Argumentos opcionales

- `antes de <fecha>` / `más de <N> días`: default, lo no leído con más de 7 días
  (`in:inbox is:unread older_than:7d`). Lo de la última semana se deja para
  `/correo-bandeja`.

## Pasos

1. Leer `correo/reglas.md`.

2. **Censo**: `mcp__Gmail__search_threads` con la query, `pageSize: 50`,
   `THREAD_VIEW_SUMMARY`, paginando hasta el final (las respuestas grandes se
   guardan en archivo: procesarlas con `jq`). Guardar por hilo `id`, `sender`,
   `subject`, `date`, `labelIds` en un JSON en el scratchpad para no volver a
   pedirlos.

3. **Agrupar** por remitente y, para remitentes automáticos de Pxsol
   (`notificaciones@`, `no-reply@`), además por tipo de asunto (CES, FQ, NPS,
   Mejoras, Egreso ONB, P0, reuniones…). Asignar a cada grupo la categoría de
   las reglas.

4. **Mostrar la tabla** ordenada por cantidad:

   ```
   🧹 Backlog: <N> hilos no leídos con más de 7 días

   #  Grupo                                   Hilos  Propuesta
   1  Promociones (varios remitentes)           35  Archivar
   2  notificaciones@pxsol.com · FQ seguim.     60  Marcar leído
   3  no-reply@pxsol.com · CES positivo         48  Marcar leído
   4  Humanos con pablo@ en Para               112  Dejar → revisar
   …
   ```

   Regla de oro: los grupos con remitentes humanos que me escriben directo,
   las alertas (P0, NPS bajo, CES negativo) y los `[NX#…]` NUNCA se archivan en
   masa; se dejan para revisión o se pasan a `/correo-pendientes`.

5. **Pedir OK** con `AskUserQuestion` (multiSelect) listando los grupos con
   propuesta "Archivar" o "Marcar leído". Pablo puede cambiar la propuesta de
   un grupo antes de aplicar.

6. **Ejecutar** por grupo con `mcp__Gmail__unlabel_thread`
   (`["INBOX"]` para archivar, `["UNREAD"]` para marcar leído,
   `["INBOX","UNREAD"]` para ambas). Informar avance cada ~50 hilos y un
   resumen final: cuántos se archivaron, cuántos se marcaron, cuántos quedan
   sin leer en la bandeja.

7. **Cerrar**: proponer reglas nuevas para `correo/reglas.md` según lo que se
   archivó (ej. "archivar siempre `news.railway.app`") y sugerir crear el
   filtro equivalente en Gmail (Configuración → Filtros) para que no vuelva a
   acumularse, dando la query exacta del filtro.

## Límites

- No borrar, no mandar a spam, no desuscribir automáticamente.
- Si el lote supera 300 hilos, confirmar de nuevo antes de seguir.
