# Backlog · Mesa de Ayuda

El setlist: el orden de los temas. Fases chicas, en orden de implementación. Cada una: una historia de Jira, un spec, un merge.

- [ ] 1 · MDA-1 Crear y consultar tickets
  - Spec: [`001-tickets`](001-tickets/spec.md). El ticket nace con identificador, estado "abierto" y fecha de creación; sin nivel ni vencimientos.
- [ ] 2 · MDA-2 Asignar y responder tickets
  - Para el spec: ¿se asigna a una persona o a un equipo? ¿La categoría define el equipo? ¿Se puede reasignar? Candidata a partir en asignar y responder.
- [ ] 3 · MDA-3 Cerrar tickets
  - Para el spec: regla candidata, un ticket cerrado rechaza nuevas respuestas. ¿Se puede reabrir? ¿Hace falta una nota de cierre?
- [ ] 4 · MDA-4 SLA por prioridad (vencimientos)
  - Para el spec: ¿SLA en horas hábiles o corridas? ¿Cuánto dura cada SLA por prioridad (baja, media, alta)? Candidata a partir en primera respuesta y resolución.
- [ ] 5 · MDA-5 Escalar de nivel (1, 2 y 3)
  - Para el spec: ¿todo ticket nace en nivel 1? ¿Se escala de a un nivel? ¿Se puede bajar de nivel? ¿Quién escala?
- [ ] 6 · MDA-6 SLA vencido: marcar y escalar
  - Para el spec: ¿cada vencimiento escala una sola vez aunque el chequeo se repita? ¿Qué pasa si el ticket ya está en nivel 3?
- [ ] 7 · MDA-7 Reportes para operaciones
  - Para el spec: ¿"abiertos por nivel" es la foto de hoy o también historial? ¿El cumplimiento de SLA se mide sobre qué período? Candidata a partir en dos reportes.

## Por qué este orden

El número de la historia en Jira no es el orden de trabajo. Este orden sale de las dependencias:

- **1** va primero: todo lo demás opera sobre tickets que ya existen.
- **2** va antes que **3**: cerrar suma la regla de rechazar respuestas en tickets cerrados.
- **4** va después de **2** y **3**: los vencimientos se miden contra la primera respuesta y el cierre.
- **5** va después de **2**: escalar cambia quién atiende un ticket ya asignado. **4** y **5** no dependen entre sí.
- **6** necesita **4** y **5**: marca lo vencido y lo escala.
- **7** va último: lee niveles y SLA.

## Cómo se usa

- Se tacha la casilla cuando se mergea la fase.
- El spec de la fase n vive en `specs/NNN-<slug>/`, con NNN el número de fase en tres dígitos. Se escribe cuando le toca, no antes.
- Entre fase y fase se revisa este archivo: qué tachar, reordenar o partir, y qué le faltó a la constitución. Si se parte una fase, cada parte conserva su MDA-n.
