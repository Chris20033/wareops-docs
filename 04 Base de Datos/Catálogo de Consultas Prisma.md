# Catálogo de Consultas Prisma

La API no usa SQL manual ni vistas. Cada consulta se encapsula en un repositorio con un selector Prisma reutilizable y devuelve un tipo inferido que un mapper convierte al DTO público.

| Consulta | Herramientas Prisma | Consumidores |
| --- | --- | --- |
| Inventario general | `findMany`, filtros relacionales y `select` de producto, almacén y sucursal | `GET /inventory` |
| Detalle de saldo | `findFirst` limitado por `warehouse.branch.organizationId` | `GET /inventory/{id}` |
| Historial | `findMany` de movimientos con `operation` y `balance.product/warehouse` | `GET /movements` |
| Saldo histórico | `_sum` de deltas anteriores y reducción de la página ordenada | Detalle y exportación futura |
| Transferencia | `findFirst` con saldos, producto, almacenes, operación y movimientos | `GET /inventory/transfers/{id}` |
| Órdenes | `findMany` con almacén, sucursal, renglones y productos | Listado y detalle de órdenes |
| Bajo mínimo | `findMany` de saldos del tenant y filtro `onHand - reserved <= minimumStock` en servicio | Dashboard y alertas |
| Dashboard | `count`, `groupBy`, `_aggregate` y consultas limitadas dentro de `$transaction` | `GET /dashboard/*` |
| Auditoría | `findMany` con actor y cambios, siempre limitado por `organizationId` | `GET /audit-events` |

## Selectores

- Cada selector declara únicamente campos públicos o necesarios para mapearlos.
- Relaciones sensibles como `passwordHash` y `tokenHash` nunca se seleccionan en consultas de presentación.
- Los filtros de tenant forman parte del repositorio y no se aceptan como opción desactivable.
- La paginación y el orden estable se aplican antes del mapper.

## Comandos

Los comandos usan `create`, `update`, `updateMany`, `upsert` y relaciones `connect` dentro de transacciones Prisma. Para inventario, `updateMany` compara `onHand` y `reserved` con los valores previamente leídos; cero filas actualizadas provoca reintento o conflicto.

## Rendimiento

Los índices se declaran con `@@index` y `@@unique`. Se seleccionan sólo columnas necesarias y se miden consultas con el dataset de demostración. No se introduce SQL especializado sin evidencia, ADR y cambio explícito de alcance.
