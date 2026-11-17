# MDA-1 — Crear y consultar tickets

Historia: [MDA-1](../../README.md#historias-cargadas-en-jira).

Este spec describe comportamiento. No elige stack, códigos de estado ni formato de error. Esos acuerdos están en [constitution.md](../../constitution.md).

## Contexto

Una persona de soporte registra un pedido de ayuda. Soporte y operaciones necesitan recuperar ese ticket por su identificador o listar tickets filtrando por estado, prioridad y cliente.

Un ticket guarda estos campos: identificador, cliente, nombre, contacto, categoría, prioridad, descripción, estado, nivel y asignación. En esta fase el estado es `abierto`, el nivel es `1` y no hay persona asignada.

## Historias

- Como persona de soporte, quiero crear un ticket con cliente, nombre, contacto, categoría, prioridad y descripción, para dejar registrado el pedido.
- Como persona de soporte u operaciones, quiero consultar un ticket por su identificador, para ver los datos con los que se creó.
- Como persona de soporte u operaciones, quiero listar tickets filtrando por estado, prioridad y cliente, para encontrar los que me importan.

## Criterios

- **R1.** When se solicita crear un ticket con cliente, nombre, contacto, categoría y descripción no vacíos después de recortar espacios, y con prioridad `baja`, `media`, `alta` o `urgente`, the system shall persistir el ticket y devolverlo con todos sus campos.
- **R2.** When el sistema crea un ticket, the system shall asignarle un identificador opaco único, estado `abierto`, nivel `1` y sin persona asignada.
- **R3.** Where dos creaciones traen los mismos datos, the system shall persistir dos tickets distintos.
- **R4.** If falta cliente, nombre, contacto, categoría o descripción, o alguno de esos textos queda vacío después de recortar espacios, then the system shall rechazar la creación y no persistir el ticket.
- **R5.** If la prioridad no es `baja`, `media`, `alta` ni `urgente`, then the system shall rechazar la creación y no persistir el ticket.
- **R6.** The system shall conservar cliente, nombre, contacto, categoría y descripción como texto, sin validar el formato del contacto.
- **R7.** When se consulta un identificador que corresponde a un ticket, the system shall devolver ese ticket con todos sus campos.
- **R8.** If el identificador consultado no corresponde a ningún ticket, then the system shall indicar que no existe.
- **R9.** When se listan tickets sin filtros, the system shall devolver todos, del más reciente al más antiguo, sin paginar.
- **R10.** When se listan tickets indicando estado, prioridad, cliente o cualquier combinación de esos filtros, the system shall devolver solo los que cumplen a la vez cada filtro presente, del más reciente al más antiguo, sin paginar.
- **R11.** When el filtro de cliente está presente, the system shall quedarse con los tickets cuyo cliente es igual al texto indicado, con la misma distinción de mayúsculas.
- **R12.** If el filtro de estado no es `abierto`, o el filtro de prioridad no es `baja`, `media`, `alta` ni `urgente`, then the system shall rechazar el listado.
- **R13.** While el sistema escribe logs, the system shall omitir el nombre y el contacto de quien reporta.

## Fuera de alcance

- Asignar y responder tickets (MDA-2).
- Cerrar tickets y anonimizar nombre y contacto (MDA-3).
- SLA por prioridad y SLA vencido (MDA-4, MDA-6).
- Escalar de nivel (MDA-5).
- Reportes para operaciones (MDA-7).
- Autenticación, paginación, edición de un ticket ya creado y validación del formato del contacto.

## Preguntas abiertas

Ninguna.
