# Diseño Lógico

## Criterios

- PostgreSQL es la base de datos y Prisma ORM es la única capa de acceso desde la API.
- `schema.prisma` define modelos, relaciones, enums, PK, FK, índices y restricciones únicas.
- Prisma Migrate genera las migraciones; no se editan manualmente.
- No se usan consultas raw, vistas, funciones, triggers ni procedimientos almacenados.
- Modelos Prisma en `PascalCase`, propiedades en `camelCase` y tablas/columnas físicas en `snake_case` mediante `@map` y `@@map`.
- UUID para identificadores públicos y `DateTime @db.Timestamptz` para fechas UTC.

## Tablas en 3FN

| Módulo | Modelos Prisma / tablas |
| --- | --- |
| Identidad y RBAC | `User`, `RefreshSession`, `Role`, `Permission`, `RolePermission` |
| Organizaciones | `Organization`, `Membership`, `Invitation` |
| Ubicaciones | `Branch`, `Warehouse` |
| Catálogo | `Product`, `Supplier`, `ProductSupplier` |
| Inventario | `InventoryBalance`, `InventoryOperation`, `InventoryMovement`, `InventoryEntry`, `Transfer` |
| Órdenes | `OutboundOrder`, `OutboundOrderLine`, `OutboundOrderOperation` |
| Plataforma | `IdempotencyRecord`, `AuditEvent`, `AuditChange` |

## Decisiones de normalización

- El correo se guarda en minúsculas en un único campo `email`; el SKU, en mayúsculas en un único campo `sku`.
- `Warehouse` obtiene la organización desde `Branch`; `InventoryBalance`, desde las relaciones con almacén y producto.
- `InventoryMovement` obtiene tenant, producto, almacén, actor y fecha mediante `InventoryBalance` e `InventoryOperation`.
- Un movimiento sólo guarda `onHandDelta` y `reservedDelta`; los saldos históricos se calculan.
- `OutboundOrderLine` obtiene almacén y organización desde `OutboundOrder`.
- Las tablas puente contienen únicamente sus FK y metadatos propios.
- `InventoryBalance` es una proyección transaccional necesaria para concurrencia; su clave natural es producto–almacén.

La demostración formal se encuentra en [[Normalización a Tercera Forma Normal]].

## Integridad expresable con Prisma

- `User.email`, `Role.code`, `Permission.code`, `Organization.slug` y `OutboundOrder.number` son únicos.
- Compuestos únicos: membresía usuario–organización, permiso–rol, proveedor–producto, saldo almacén–producto, movimiento por operación–saldo, producto por orden, orden–operación y clave idempotente por organización.
- Los enums limitan estados y tipos cerrados.
- Las FK usan integridad referencial de PostgreSQL generada por Prisma.
- Cantidades, transiciones, pertenencia al mismo tenant, último propietario y compatibilidad entre tipo de operación y deltas se validan en servicios de dominio porque Prisma Schema no expresa esas reglas completas.

## Consultas

Los repositorios usan `select`, `include`, filtros relacionales, `count`, `groupBy` y `_aggregate`. Los mappers convierten el resultado normalizado a DTO; no se expone el modelo Prisma al controlador. Véase [[Catálogo de Consultas Prisma]].

## Concurrencia

Las operaciones críticas usan una transacción interactiva Prisma con aislamiento `Serializable`. Dentro de ella se leen y validan todos los saldos, y cada actualización usa comparación con los valores observados. Un conflicto `P2034` reintenta la transacción completa hasta tres veces; después se devuelve `409 CONCURRENT_MODIFICATION`.

Saldos, movimientos, auditoría e idempotencia se confirman o revierten como unidad. No se realizan llamadas de red dentro de la transacción.

## Índices principales

- Membresías por usuario/estado y organización/rol/estado.
- Catálogos por organización/estado y campos de búsqueda.
- Saldos por almacén y producto.
- Operaciones por actor/tipo/fecha y movimientos por operación/saldo.
- Órdenes por almacén/estado/fecha.
- Auditoría e idempotencia por organización/fecha.

Véase [[Diccionario de Datos]] y [[../07 Diagramas/Modelo ER|Modelo ER]].
