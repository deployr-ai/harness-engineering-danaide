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

Todos los datos del proyecto son sintéticos: no uses datos reales de personas ni de sistemas.
