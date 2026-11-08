# Cierre semanal del equipo PMS

Panel y automatismo para seguir lo trabajado cada semana por Nacho, Nadia e Iara y llevar el OKR Q4-26.

- **Panel**: [Semana Equipo PMS](https://claude.ai/artifact/SZ9sRMv3VYVVncz338NnEg). Tickets cerrados, CES y OKR salen de Nexus en vivo; minimejoras, reuniones con cliente + entregable (grabadas en Nexus por ellos o por Pablo, con la persona participando y al menos una minimejora o proyecto), entrevistas internas y proyectos salen del cierre semanal. Las reuniones grabadas sin proyecto ni minimejora aparecen como alerta con una sugerencia de qué puede salir.
- **Automatismo**: tarea programada los viernes 17:40 (Argentina) que sigue `SKILL.md`: clasifica la semana, actualiza el panel y deja a Pablo un borrador de mail con el cierre y el check-in propuesto. No carga nada en Nexus sin confirmación.
- **Cargar el OKR**: con el OK de Pablo, `/cierresemanal cargar` hace el check-in de los KRs manuales y etiqueta las minimejoras.

## Archivos

| Archivo | Qué es |
|---|---|
| `SKILL.md` | Procedimiento completo del cierre (fuentes, reglas de clasificación, panel, mail, carga). |
| `equipo.json` | Personas, ids de Nexus, nombres de KRs, URL del panel. |
| `data/resumen.json` | Totales por semana y persona (lo que lee el panel). |
| `data/evidencias.json` | Cada reunión, minimejora, entrevista o proyecto contado, con su entregable y estado. |

## Para que el conteo salga solo

Lo que más cuesta reconstruir son las minimejoras. Si el equipo pone la etiqueta `minimejora` en el ticket al entregarla, el cierre la cuenta como confirmada sin pedir revisión.
