# Constitución

Acuerdos del proyecto Mesa de Ayuda. Cambian poco y solo con acuerdo del equipo.

## Misión y audiencia

Mesa de Ayuda es una API interna para gestionar tickets de soporte. La usan las personas de soporte y de operaciones. Quien reporta el problema queda registrado como dato del ticket (cliente, nombre y contacto); no es un usuario de la API.

## Stack

Python con FastAPI, PostgreSQL, pruebas con pytest y ejecución con Docker Compose. Las versiones se eligen al implementar. Los specs de cada fase no deciden stack: el stack vive acá.

## Calidad

Cada fase se verifica con tests de comportamiento de la API contra PostgreSQL real, levantado con Docker Compose. La cobertura de líneas del código de la aplicación es al menos 80%. Quedan fuera de esa medida los tests y las migraciones.

## Seguridad y datos

Estas fases no exigen autenticación. Quien llega a la API puede crear y leer tickets. Todos los datos del proyecto son sintéticos: no se usan datos reales de personas ni de sistemas. El nombre y el contacto de quien reporta no se escriben en los logs. Al cerrar un ticket (MDA-3) se anonimizan el nombre y el contacto; el resto del ticket permanece.

## Forma de trabajo

El orden de trabajo está en [specs/backlog.md](specs/backlog.md): fases chicas, en orden de implementación, una historia `MDA-n` por fase. Se revisa entre fase y fase. Se implementa una fase por vez, la primera casilla sin marcar.

Antes de escribir código de una fase existe su spec en `specs/NNN-<slug>/spec.md`. Los requisitos del spec usan la sintaxis EARS y llevan ids `R1`, `R2`, y así sucesivamente. El spec describe comportamiento. No elige framework, base de datos ni formato de error.
