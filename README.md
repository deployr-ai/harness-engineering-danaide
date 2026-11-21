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

## Cómo arranca cada grupo

Cada grupo trabaja en su propio fork de este repo. Este repo queda con el punto de partida y para
las demos de clase.

1. Un integrante hace el fork con el nombre `harness-engineering-danaide-grupo-NN` (por ejemplo,
   `harness-engineering-danaide-grupo-03`, con el número del Sheet de grupos) y suma al resto del
   grupo como colaboradores (Settings, Collaborators).
2. Cada integrante clona el fork: `git clone https://github.com/<usuario>/harness-engineering-danaide-grupo-NN.git`.
3. Una rama por fase, con la clave de la historia en el nombre: `git switch -c MDA-1-tickets`.
4. El PR va al `main` **del fork**. Al abrirlo, GitHub propone como destino este repo: cambiar
   "base repository" por el fork del grupo.
5. Otro integrante revisa el PR y el grupo lo mergea. Ese merge cierra la fase.
6. El link del fork va en la columna **Fork (GitHub)** del Sheet de grupos.

Para los gates en CI, habilitar las Actions en la pestaña **Actions** del fork: GitHub las deja
apagadas en los forks. Si este README cambia después de hacer el fork, el botón **Sync fork** trae
los cambios.

**¿El grupo no llegó con su spec 001?** La rama `referencia/clase-01` trae constitución, setlist y
spec 001, sin código. Un fork hecho solo con `main` (la opción que GitHub deja tildada) no la tiene,
y **Sync fork** tampoco la trae. Para arrancar MDA-1 desde ahí:

```bash
git remote add upstream https://github.com/deployr-ai/harness-engineering-danaide.git
git fetch upstream referencia/clase-01
git switch -c MDA-1-tickets upstream/referencia/clase-01
```

Antes de la clase 3, el grupo reescribe la constitución con su propia entrevista.

## Cómo trabajamos

- `constitution.md`: los acuerdos del proyecto. Cambian poco y con acuerdo del equipo.
- `specs/backlog.md`: el orden de los temas. Fases chicas, en orden de implementación, cada una con
  su historia `MDA-n`. El orden y el tamaño de las fases los decide el equipo. Se revisa entre fase
  y fase.
- `specs/NNN-<tema>/spec.md`: el spec de cada fase, antes de escribir código.

Todos los datos del proyecto son sintéticos: no uses datos reales de personas ni de sistemas.
