# Spec 001 · Crear y consultar tickets

Historia: **MDA-1** · Fase 1 del [backlog](../backlog.md)

## Contexto y problema

Soporte recibe pedidos de clientes sin un lugar único donde registrarlos. Sin un registro no se
puede asignar, responder ni medir nada. Esta fase permite registrar un ticket y volver a
consultarlo, con visibilidad según el rol de cada usuario.

- Roles: cliente final, agente de soporte, operaciones y administrador.
- Los usuarios internos pertenecen a un sector (área interna: soporte, producto, operaciones).
- El cliente se identifica por nombre, email de contacto y empresa (datos sintéticos). El email
  vincula al cliente final con sus tickets.
- Cada ticket pertenece a un sector, que se deduce de su categoría:

  | Categoría             | Sector   |
  |-----------------------|----------|
  | Acceso y cuentas      | Soporte  |
  | Consulta              | Soporte  |
  | Incidente técnico     | Soporte  |
  | Solicitud de cambio   | Producto |

## Historias

- Como agente de soporte quiero crear tickets para registrar los pedidos de los clientes.
- Como agente de soporte quiero consultar y listar los tickets de mi sector para saber qué hay
  pendiente.
- Como operaciones quiero consultar y listar todos los tickets para seguir cómo viene el trabajo.
- Como cliente final quiero consultar mis tickets para saber en qué quedaron mis pedidos.

## Criterios de aceptación

### Creación

- **R1.** El sistema DEBE exigir cliente (nombre, email de contacto y empresa), categoría,
  prioridad y descripción para crear un ticket.
- **R2.** SI falta alguno de los campos obligatorios, o está vacío o tiene solo espacios, ENTONCES
  el sistema DEBE rechazar el ticket.
- **R3.** SI la categoría no es acceso y cuentas, consulta, solicitud de cambio o incidente
  técnico, ENTONCES el sistema DEBE rechazar el ticket.
- **R4.** SI la prioridad no es baja, media, alta o crítica, ENTONCES el sistema DEBE rechazar el
  ticket.
- **R5.** SI el email de contacto no tiene formato de email, ENTONCES el sistema DEBE rechazar el
  ticket.
- **R6.** SI quien crea el ticket no es agente de soporte ni administrador, ENTONCES el sistema
  DEBE rechazarlo por falta de permiso.
- **R7.** CUANDO se crea un ticket, el sistema DEBE asignarle un identificador único.
- **R8.** CUANDO se crea un ticket, el sistema DEBE dejarlo en estado abierto.
- **R9.** CUANDO se crea un ticket, el sistema DEBE dejarlo en nivel 1.
- **R10.** CUANDO se crea un ticket, el sistema DEBE registrar su fecha de creación.
- **R11.** CUANDO se crea un ticket, el sistema DEBE registrar qué usuario lo creó.
- **R12.** CUANDO se crea un ticket, el sistema DEBE asignarle el sector que corresponde a su
  categoría, según la tabla del contexto.

### Identificación

- **R13.** SI el pedido no identifica a un usuario con un rol válido (cliente final, agente de
  soporte, operaciones o administrador), ENTONCES el sistema DEBE rechazarlo.

### Consulta y visibilidad

- **R14.** CUANDO se consulta un ticket visible para el usuario, el sistema DEBE devolver todos sus
  datos.
- **R15.** SI se consulta un ticket que no existe, ENTONCES el sistema DEBE informar que no se
  encontró.
- **R16.** MIENTRAS quien consulta es un cliente final, el sistema DEBE limitar consultas y
  listados a los tickets cuyo email de contacto coincide con el suyo.
- **R17.** MIENTRAS quien consulta es un agente de soporte, el sistema DEBE limitar consultas y
  listados a los tickets de su sector.
- **R18.** MIENTRAS quien consulta es operaciones o administrador, el sistema DEBE permitir ver
  todos los tickets.
- **R19.** SI un usuario consulta un ticket fuera de su visibilidad, ENTONCES el sistema DEBE
  informar que no se encontró.

### Listado

- **R20.** CUANDO se pide el listado, el sistema DEBE devolver los tickets ordenados por fecha de
  creación, del más reciente al más antiguo, y ante igual fecha por identificador descendente.
- **R21.** CUANDO se pide el listado, el sistema DEBE entregarlo por páginas de 20 tickets por
  defecto y permitir pedir hasta 100 por página.
- **R22.** SI se piden más de 100 tickets por página, ENTONCES el sistema DEBE rechazar el pedido.
- **R23.** SI se pide una página posterior a la última, ENTONCES el sistema DEBE devolver una lista
  vacía.
- **R24.** DONDE el listado se filtre por estado, categoría o prioridad, el sistema DEBE devolver
  solo los tickets que cumplen todos los filtros indicados.
- **R25.** SI un filtro trae un valor que no existe para ese campo, ENTONCES el sistema DEBE
  rechazar el pedido.

## Fuera de alcance

- Compartir un ticket puntual con otro usuario (pendiente de acordar con Martín; no tiene historia
  MDA-n).
- Gestionar usuarios, roles y sectores (alta, baja, cambios).
- Asignar, responder, cerrar o escalar tickets (MDA-2, 3 y 5).
- Vencimientos de SLA (MDA-4).
- Editar o borrar tickets: los tickets no se borran.
- Chat con el cliente y facturación.

## Decisiones tomadas

Propuestas en la revisión del spec; las firma el equipo al revisar el PR de esta fase.

1. **El contacto del cliente es un email obligatorio** y es lo que vincula al cliente final con sus
   tickets (R5, R16). Sin un vínculo explícito, R16 no se podía implementar ni testear.
2. **El sector del ticket sale de su categoría** (tabla del contexto, R12). Es el supuesto que ya
   tenía el spec, ahora con una regla concreta.
3. **Operaciones ve todos los tickets** (R18). Sofía necesita ver todo el trabajo para los
   reportes de MDA-7; limitarla a un sector obligaba a romper la regla en esa fase.
4. **Solo agente de soporte y administrador crean tickets** (R6). El cliente final solo consulta.
5. **Todo pedido identifica a un usuario con rol** (R13). Cómo se identifica se resuelve en el
   plan.
6. **Un texto vacío o con solo espacios cuenta como faltante** (R2).
7. **El orden del listado tiene desempate por identificador** (R20), para que la paginación no
   repita ni saltee tickets.
8. **Páginas de 20 por defecto y 100 como máximo** (R21 a R23).
9. **Los filtros se combinan con Y y un valor inexistente se rechaza** (R24, R25), para que un
   error de tipeo no parezca un listado vacío.
10. **El ticket nace en nivel 1 y registra quién lo creó** (R9, R11). MDA-5 y MDA-7 trabajan con
    niveles; definirlo ahora evita una migración.
11. **Los roles se nombran siempre igual**: cliente final, agente de soporte, operaciones y
    administrador.

## Preguntas abiertas

- Ninguna bloquea esta fase. Compartir tickets queda anotado en el backlog.
