# Backlog · Mesa de Ayuda

Fases chicas, en orden de implementación. Cada una: una historia, un spec, un merge.
Se revisa entre fase y fase.

- [ ] 1 · MDA-1 Crear y consultar tickets
- [ ] 2 · MDA-2 Asignar y responder tickets
- [ ] 3 · MDA-3 Cerrar tickets
- [ ] 4 · MDA-4 SLA por prioridad: vencimientos de primera respuesta y de resolución
- [ ] 5 · MDA-5 Escalar de nivel (1, 2 y 3)
- [ ] 6 · MDA-6 SLA vencido: marcar el ticket y escalarlo
- [ ] 7 · MDA-7 Reportes para operaciones: abiertos por nivel y cumplimiento de SLA

## Por qué este orden

- Primero el ciclo de vida básico (1 a 3): sin tickets no hay nada que medir.
- MDA-4 antes que MDA-6: no se puede marcar un SLA vencido sin vencimientos.
- MDA-5 antes que MDA-6: el escalamiento automático reutiliza el manual.
- MDA-7 al final: los reportes leen datos que producen todas las fases anteriores.

## Anotado para después

- Compartir un ticket puntual con otro usuario: sin historia MDA-n; acordar con Martín.
- MDA-4: el SLA corre en horas corridas (24/7). Se confirma en el spec de esa fase.
- MDA-7: operaciones ya ve todos los tickets desde MDA-1 (spec 001, R18).
