# Spec 001 · Crear y consultar tickets

- **Historia de Jira:** MDA-1 · Crear y consultar tickets
- **Fase:** 1 de [`specs/backlog.md`](../backlog.md)
- **Constitución:** [`constitution.md`](../../constitution.md)

## Contexto y problema

Mesa de Ayuda arranca sin tickets. Soporte necesita registrar los pedidos de los clientes y poder volver a encontrarlos. Sin ese registro no hay nada que asignar, responder, escalar, medir ni reportar (MDA-2 a MDA-7). Esta fase es el cimiento: crear tickets y consultarlos.

Este spec dice qué hace el sistema y por qué. El cómo (tecnología, interfaces, almacenamiento) va en el plan.

## Historias

- **H1.** Como agente de soporte, quiero crear un ticket con los datos del cliente, la categoría, la prioridad y la descripción, para registrar su pedido.
- **H2.** Como agente de soporte, quiero consultar un ticket por su identificador, para retomar un pedido sin volver a preguntarle al cliente.
- **H3.** Como agente de soporte o de operaciones, quiero ver el listado de tickets, del más reciente al más antiguo, para saber qué pedidos entraron.

## Criterios de aceptación

Los ids son estables: no se renumeran. Cada criterio se vuelve al menos un test con el mismo id.

### Términos

- **Ticket:** el pedido de un cliente. Sus datos son: identificador, nombre del cliente, contacto del cliente, categoría, prioridad, descripción, estado, y fecha y hora de creación.
- **Datos obligatorios al crear:** nombre del cliente, contacto del cliente, categoría, prioridad y descripción. El identificador, el estado y la fecha los asigna el sistema.
- **Vacío:** sin texto o solo con espacios.
- **Datos válidos:** los cinco datos obligatorios presentes y no vacíos, con categoría y prioridad entre los valores permitidos.
- **Prioridades permitidas:** baja, media, alta.
- **Categorías permitidas:** acceso, incidente, consulta, solicitud (propuesta, ver P1).
- **Rechazar la creación:** no registrar ningún ticket.

### Crear un ticket

- **R1.** CUANDO se crea un ticket con datos válidos, el sistema DEBE devolver el ticket creado con los datos recibidos.
- **R2.** SI algún dato obligatorio falta o está vacío, ENTONCES el sistema DEBE rechazar la creación.
- **R3.** SI la categoría o la prioridad no están entre los valores permitidos, ENTONCES el sistema DEBE rechazar la creación.
- **R4.** SI se rechaza la creación, ENTONCES el sistema DEBE informar cuáles datos faltan o son inválidos.
- **R5.** El sistema DEBE asignar a cada ticket un identificador único.
- **R6.** CUANDO se crea un ticket, el sistema DEBE dejarlo en estado "abierto".
- **R7.** CUANDO se crea un ticket, el sistema DEBE registrar su fecha y hora de creación, en UTC.

### Consultar tickets

- **R8.** CUANDO se consulta un ticket por su identificador, el sistema DEBE devolver el ticket con todos sus datos.
- **R9.** SI el identificador consultado no corresponde a ningún ticket, ENTONCES el sistema DEBE informar que el ticket no existe.
- **R10.** CUANDO se pide el listado de tickets, el sistema DEBE devolver todos los tickets, del más reciente al más antiguo.
- **R11.** SI no hay ningún ticket, ENTONCES el sistema DEBE devolver un listado vacío.

## Fuera de alcance

Lo que este tema no toca:

- Asignar y responder tickets (MDA-2).
- Cerrar tickets (MDA-3). Por eso "abierto" es el único estado de esta fase.
- Vencimientos y SLA (MDA-4) y SLA vencido (MDA-6). Al crear un ticket no se calcula ningún vencimiento.
- Niveles y escalamiento (MDA-5). El ticket todavía no tiene nivel.
- Reportes (MDA-7).
- Editar los datos de un ticket ya creado: no está en ninguna historia.
- Borrar tickets: el proyecto no los borra (constitución).
- Autenticación y roles (constitución).

## Preguntas abiertas

- **P1.** Categorías y prioridades: ¿son las propuestas (acceso, incidente, consulta, solicitud; baja, media, alta)? ¿Se acepta "Alta" con mayúscula?
- **P2.** Contacto del cliente: ¿email, teléfono o texto libre? ¿Se valida el formato? Hoy R2 solo exige que no esté vacío.
- **P3.** ¿Hay un largo máximo para el nombre, el contacto y la descripción?
- **P4.** Listado: ¿hacen falta filtros (estado, prioridad, categoría, cliente) y paginación? Hoy R10 devuelve todo.
- **P5.** ¿Se permiten dos tickets idénticos o se avisa de un posible duplicado? Hoy se permiten.
- **P6.** Identificador: ¿un número correlativo que se pueda dictar por teléfono o un código opaco?
- **P7.** Estados: esta fase solo define "abierto". ¿Conviene fijar el ciclo de vida completo (estados y transiciones) antes de MDA-2 y MDA-3?
