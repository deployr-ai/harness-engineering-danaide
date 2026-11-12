# Mesa de Ayuda

Una API para gestionar tickets de soporte con SLA y escalamiento. Este repo arranca vacío: lo
construimos entre todos, de a una fase por vez, trabajando con un agente de código.

## Input de los stakeholders

- Lucía, de ingeniería, quiere un servicio confiable sobre un stack popular y fácil de mantener:
  Python con FastAPI, PostgreSQL como base de datos, pruebas con pytest y todo corriendo con Docker
  Compose.
- Martín, de producto, tiene un conjunto de funcionalidades sobre tickets: crearlos (cliente,
  categoría, prioridad, descripción), asignarlos, responderlos, escalarlos de nivel (1, 2 y 3) y
  cerrarlos. Cada prioridad tiene un SLA de primera respuesta y de resolución; cuando un SLA se
  vence, el ticket se marca y se escala.
- Sofía, de operaciones, quiere ver cómo viene el trabajo: tickets abiertos por nivel y
  cumplimiento de SLA.

## Historias cargadas en Jira

Martín ya cargó estas historias. Las claves son las de Jira; el número no es el orden de trabajo.

- **MDA-1** Crear y consultar tickets.
- **MDA-2** Asignar y responder tickets.
- **MDA-3** Cerrar tickets.
- **MDA-4** SLA por prioridad: vencimientos de primera respuesta y de resolución.
- **MDA-5** Escalar de nivel (1, 2 y 3).
- **MDA-6** SLA vencido: marcar el ticket y escalarlo.
- **MDA-7** Reportes para operaciones: abiertos por nivel y cumplimiento de SLA.

## Cómo trabajamos

- `constitution.md`: los acuerdos del proyecto. Cambian poco y con acuerdo del equipo.
- `specs/backlog.md`: el orden de los temas. Fases chicas, en orden de implementación, cada una con
  su historia `MDA-n`. El orden y el tamaño de las fases los decide el equipo. Se revisa entre fase
  y fase.
- `specs/NNN-<tema>/spec.md`: el spec de cada fase, antes de escribir código.

Todos los datos del proyecto son sintéticos: no uses datos reales de personas ni de sistemas.
