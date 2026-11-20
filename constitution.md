# Constitución · Mesa de Ayuda

Acuerdos del proyecto. Los leen personas y agentes. Cambian poco y solo con acuerdo del equipo.

## Misión y audiencia

API para gestionar tickets de soporte con SLA por prioridad y escalamiento en tres niveles.

- Usan la API: soporte y producto (Martín), operaciones (Sofía) y el cliente final.
- La mantiene ingeniería (Lucía).
- No hace: chat con el cliente ni facturación.

## Stack

- Python 3.12 + FastAPI
- PostgreSQL (SQLite en tests)
- pytest
- Docker Compose: todo el servicio levanta con `docker compose up`

## Calidad

- Primero el test: cada criterio `R<n>` del spec tiene al menos un test con el mismo id.
- Todo cambio entra por PR al `main` del fork, revisado por otro integrante del grupo.
- Un PR cubre una sola fase y cita los criterios que implementa.

## Seguridad y datos

- Solo datos sintéticos: nada de personas ni sistemas reales, incluidos los datos personales de
  quien reporta.
- De quien reporta se guardan nombre, contacto y empresa, y nada más.
- Ningún secreto en el repo: la configuración va por variables de entorno.
- Los tickets no se borran, tampoco los cerrados.
- El acceso a los tickets depende del rol (cliente final, soporte, operaciones, administrador) y,
  en usuarios internos, de su sector.

## Forma de trabajo

- El orden de trabajo vive en `specs/backlog.md`: fases chicas, una por historia `MDA-n`.
- Un spec por fase en `specs/NNN-<tema>/spec.md`, escrito antes del código.
- Los specs describen el qué y el porqué, sin decisiones de stack (eso va en el plan).
- Si cambia el comportamiento, cambia primero el spec.
- Ramas con la clave de la historia: `MDA-1-tickets`.
- El agente propone, el equipo firma.
