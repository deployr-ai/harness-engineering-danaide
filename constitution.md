# Constitución · Mesa de Ayuda

Los acuerdos del proyecto: lo que no se negocia. La leen personas y agentes. Cambia poco y solo con acuerdo del equipo. El orden de trabajo vive aparte, en [`specs/backlog.md`](specs/backlog.md).

## Misión y audiencia

API de tickets de soporte con SLA por prioridad y escalamiento en tres niveles.

- **Audiencia:** soporte y producto (Martín), operaciones (Sofía). La mantiene ingeniería (Lucía). Es de uso interno: el cliente final no usa el sistema, es un dato del ticket.
- **Lo que no hace:** el chat con el cliente y la facturación. Autenticación y roles quedan fuera por ahora; entran solo con un acuerdo explícito que cambie esta constitución.

## Stack

Python 3.12 + FastAPI · PostgreSQL (SQLite en los tests) · pytest · Docker Compose.

## Calidad

- Primero el test. Cada criterio `R<n>` del spec tiene al menos un test con el mismo id.
- Todo cambio entra por pull request, con revisión humana de otra persona del equipo.
- Fechas y horas siempre en UTC.
- Todavía no hay gates automáticos acordados (lint, CI): no se agregan hasta acordarlos.

## Seguridad y datos

- Solo datos sintéticos: ningún dato real de personas ni de sistemas, ni en el repo ni en lo que se le pega al agente.
- De quien reporta se guarda nombre y contacto, y nada más.
- Ningún secreto en el repo: la configuración va por variables de entorno.
- Los tickets no se borran: se cierran.

## Forma de trabajo

- El orden de trabajo vive en `specs/backlog.md`: fases chicas, una por historia MDA-n.
- Un spec por fase, en `specs/NNN-<slug>/spec.md`, enlazado a su historia y escrito antes del código.
- Si el comportamiento cambia, cambia primero el spec.
- Una rama por fase, con la clave de la historia en el nombre (por ejemplo, `MDA-1-tickets`). El pull request va al `main` del fork del grupo, lo revisa otra persona y el merge cierra la fase.
- El agente propone; el equipo firma.
- Idioma: español para la documentación y el dominio (campos, mensajes, tests).
