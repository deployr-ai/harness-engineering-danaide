# Spec 001 · Crear y consultar tickets

Historia: **MDA-1** · Fase 1 del [backlog](../backlog.md)

## Contexto y problema

Soporte recibe pedidos de clientes sin un lugar único donde registrarlos. Sin un registro no se
puede asignar, responder ni medir nada. Esta fase permite registrar un ticket y volver a
consultarlo, con visibilidad según el rol de cada usuario.

- Roles: cliente final, agente de soporte, operaciones y administrador.
- Los usuarios internos pertenecen a un sector (área interna: soporte, producto, operaciones).
- El cliente se identifica por nombre, contacto y empresa (datos sintéticos).

## Historias

- Como agente de soporte quiero crear tickets para registrar los pedidos de los clientes.
- Como usuario interno quiero consultar y listar los tickets de mi sector para saber qué hay
  pendiente.
- Como cliente final quiero consultar mis tickets para saber en qué quedaron mis pedidos.

## Criterios de aceptación

- **R1.** El sistema DEBE exigir cliente (nombre, contacto y empresa), categoría, prioridad y
  descripción para crear un ticket.
- **R2.** SI falta alguno de los campos obligatorios, ENTONCES el sistema DEBE rechazar el ticket.
- **R3.** SI la categoría no es acceso y cuentas, consulta, solicitud de cambio o incidente
  técnico, ENTONCES el sistema DEBE rechazar el ticket.
- **R4.** SI la prioridad no es baja, media, alta o crítica, ENTONCES el sistema DEBE rechazar el
  ticket.
- **R5.** CUANDO se crea un ticket, el sistema DEBE asignarle un identificador único.
- **R6.** CUANDO se crea un ticket, el sistema DEBE dejarlo en estado abierto.
- **R7.** CUANDO se crea un ticket, el sistema DEBE registrar su fecha de creación.
- **R8.** CUANDO se consulta un ticket visible para el usuario, el sistema DEBE devolver todos sus
  datos.
- **R9.** SI se consulta un ticket que no existe, ENTONCES el sistema DEBE informar que no se
  encontró.
- **R10.** El sistema DEBE asignar a cada usuario un rol: cliente final, agente de soporte,
  operaciones o administrador.
- **R11.** MIENTRAS quien consulta es un cliente final, el sistema DEBE limitar consultas y
  listados a sus propios tickets.
- **R12.** MIENTRAS quien consulta es un agente de soporte o de operaciones, el sistema DEBE
  limitar consultas y listados a los tickets de su sector.
- **R13.** MIENTRAS quien consulta es un administrador, el sistema DEBE permitir ver todos los
  tickets.
- **R14.** SI un usuario consulta un ticket fuera de su visibilidad, ENTONCES el sistema DEBE
  informar que no se encontró.
- **R15.** CUANDO se pide el listado, el sistema DEBE devolver los tickets ordenados del más
  reciente al más antiguo.
- **R16.** CUANDO se pide el listado, el sistema DEBE entregarlo por páginas.
- **R17.** DONDE el listado se filtre por estado, categoría o prioridad, el sistema DEBE devolver
  solo los tickets que coinciden.

## Fuera de alcance

- Compartir un ticket puntual con otro usuario (pendiente de acordar con Martín; no tiene historia
  MDA-n).
- Gestionar roles y sectores (alta, baja, cambios).
- Asignar, responder, cerrar o escalar tickets (MDA-2, 3 y 5).
- Vencimientos de SLA (MDA-4).
- Editar o borrar tickets: los tickets no se borran.
- Chat con el cliente y facturación.

## Preguntas abiertas

- ¿Cómo se determina el sector de un ticket? (Supuesto: según su categoría.)
- ¿Cómo se identifica al usuario y su rol en cada pedido? (Se resuelve en el plan, pero define qué
  se puede testear en R11 a R14.)
- ¿Puede el cliente final crear tickets, o solo consultarlos? (Supuesto: solo soporte y
  administrador crean.)
- ¿Cuántos tickets por página?
- ¿Qué formato tiene el contacto del cliente: email, teléfono o ambos?
