# Normalización a Tercera Forma Normal

## Objetivo

El esquema evita grupos repetidos, dependencias parciales y dependencias transitivas. La API reconstruye DTO útiles mediante relaciones Prisma, no duplicando columnas.

## Primera forma normal

- Cada fila tiene una PK estable.
- Cada columna contiene un valor escalar de su tipo.
- Productos por orden, proveedores por producto, permisos por rol y cambios de auditoría se representan en tablas hijas o puente.
- No se almacenan listas de IDs ni objetos de negocio dentro de JSON.

`IdempotencyRecord.responseBody` es un artefacto técnico opaco de reproducción, no una relación consultable del dominio.

## Segunda forma normal

Las tablas con clave compuesta sólo contienen atributos dependientes de la clave completa:

| Tabla | Clave | Dependencia completa |
| --- | --- | --- |
| `RolePermission` | rol + permiso | No contiene atributos propios. |
| `ProductSupplier` | producto + proveedor | Sólo fecha de creación de esa asociación. |
| `OutboundOrderOperation` | orden + operación | No contiene datos de orden ni operación. |
| `OutboundOrderLine` | ID; única orden + producto | Cantidad depende del producto dentro de esa orden. |

## Tercera forma normal

| Relación | Dependencia preservada | Datos eliminados por ser derivables |
| --- | --- | --- |
| `Warehouse → Branch → Organization` | El almacén guarda sólo `branchId`. | `organizationId`. |
| `Balance → Warehouse/Product` | El saldo guarda sus dos FK. | Organización, nombre, SKU y disponibilidad. |
| `Movement → Operation/Balance` | El movimiento guarda operación, saldo y deltas. | Actor, fecha, tenant, producto, almacén y saldos posteriores. |
| `OrderLine → Order/Product` | El renglón guarda sus dos FK y cantidad. | Organización y almacén. |
| `Membership → Role` | La membresía guarda `roleId`. | Nombre del rol y permisos. |
| `AuditChange → AuditEvent` | El cambio guarda evento, campo y valores. | Actor, tenant, acción y entidad. |

## Proyecciones deliberadas

`InventoryBalance` conserva el estado actual aunque pueda reconstruirse desde movimientos. Se trata como una proyección transaccional independiente con la clave natural almacén–producto; permite validar y actualizar inventario sin recorrer todo el ledger. El servicio actualiza saldo y movimientos en la misma transacción.

## Integridad entre tenants

Al retirar claves de organización derivables, algunas relaciones no admiten una restricción compuesta directa sin volver a introducir redundancia. Antes de cualquier `connect`, el servicio consulta las relaciones completas con Prisma y confirma que todas terminan en la organización activa. Las pruebas de integración cubren cada relación cruzable.

## Regla de evolución

Una columna duplicada sólo podrá incorporarse después de medir un problema, registrar un ADR y definir cómo se mantendrá consistente. La comodidad de una consulta no justifica romper 3FN; para ella se crean selectores y mappers Prisma.
