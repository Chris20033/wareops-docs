# Sprint 06 — Supervisión

**Estado:** Pending  
**Objetivo:** convertir las operaciones registradas en información útil y auditable.

## Dependencias

Sprints 01–05 completados.

## Backend

- [ ] Implementar conteo de productos activos del dashboard.
- [ ] Implementar conteo de almacenes activos del dashboard.
- [ ] Implementar conteo de órdenes agrupado por estado.
- [ ] Implementar consulta de productos bajo mínimo.
- [ ] Calcular bajo mínimo con `onHand - reserved <= minimumStock`.
- [ ] Implementar consulta de movimientos recientes.
- [ ] Limitar la actividad reciente al tenant activo.
- [ ] Implementar creación de `AuditEvent` para mutaciones sensibles faltantes.
- [ ] Implementar creación de `AuditChange` por campo auditado.
- [ ] Aplicar redacción de campos sensibles antes de crear `AuditChange`.
- [ ] Implementar listado paginado de auditoría.
- [ ] Implementar filtro de auditoría por fecha.
- [ ] Implementar filtro de auditoría por actor.
- [ ] Implementar filtro de auditoría por acción.
- [ ] Implementar filtro de auditoría por tipo de entidad.
- [ ] Implementar filtro de auditoría por ID de entidad.
- [ ] Implementar detalle de evento de auditoría.
- [ ] Restringir auditoría al permiso `audit:read`.
- [ ] Restringir dashboard al permiso `dashboard:read`.

## Frontend

- [ ] Crear página principal de dashboard.
- [ ] Crear tarjeta de productos activos.
- [ ] Crear tarjeta de almacenes activos.
- [ ] Crear tarjeta de órdenes por estado.
- [ ] Crear sección de alertas de mínimo.
- [ ] Crear sección de movimientos recientes.
- [ ] Crear enlace de alerta al detalle de inventario.
- [ ] Crear listado de auditoría.
- [ ] Crear filtros de fecha para auditoría.
- [ ] Crear filtro de actor para auditoría.
- [ ] Crear filtro de acción para auditoría.
- [ ] Crear filtro de entidad para auditoría.
- [ ] Sincronizar filtros y página de auditoría con la URL.
- [ ] Crear detalle de evento de auditoría.
- [ ] Mostrar cambios auditados en formato legible.
- [ ] Ocultar navegación de auditoría sin `audit:read`.

## Datos e Infraestructura

- [ ] Añadir índices Prisma de auditoría definidos en el diccionario.
- [ ] Añadir índices Prisma para consultas del dashboard.
- [ ] Crear datos seed con productos bajo mínimo.
- [ ] Crear datos seed con actividad reciente.
- [ ] Crear datos seed con eventos y cambios de auditoría.

## Documentación

- [ ] Documentar resumen de dashboard en OpenAPI.
- [ ] Documentar alertas de mínimo en OpenAPI.
- [ ] Documentar movimientos recientes en OpenAPI.
- [ ] Documentar listado de auditoría en OpenAPI.
- [ ] Documentar filtros de auditoría en OpenAPI.
- [ ] Documentar detalle de evento de auditoría en OpenAPI.
- [ ] Sincronizar campos auditados y redactados con el diccionario.

## Pruebas

- [ ] Probar que los conteos del dashboard sólo incluyen el tenant activo.
- [ ] Probar que las alertas se generan por producto y almacén.
- [ ] Probar que una disponibilidad igual al mínimo genera alerta.
- [ ] Probar que una disponibilidad mayor al mínimo no genera alerta.
- [ ] Probar que actividad reciente no incluye otros tenants.
- [ ] Probar que una mutación sensible crea `AuditEvent`.
- [ ] Probar que cada campo permitido crea `AuditChange`.
- [ ] Probar que secretos no aparecen en auditoría.
- [ ] Probar filtro de auditoría por fecha.
- [ ] Probar filtro de auditoría por actor.
- [ ] Probar filtro de auditoría por acción.
- [ ] Probar filtro de auditoría por entidad.
- [ ] Probar que `OPERATOR` no consulta auditoría.
- [ ] Probar que los roles autorizados consultan dashboard.

**Trazabilidad:** RF-030–033; RNF-004, RNF-010–012, RNF-022; CA-002, CA-018–020.

## Cierre del sprint

- [ ] El dashboard refleja los datos semilla y cada paso del recorrido principal puede reconstruirse desde movimientos y auditoría.
