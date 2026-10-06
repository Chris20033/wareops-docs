# Entidades del Dominio

## Identidad y acceso

| Entidad | Responsabilidad | Relaciones principales |
| --- | --- | --- |
| `User` | Identidad global y credenciales de una persona. | Tiene membresías y sesiones. |
| `Organization` | Límite de aislamiento de una empresa. | Agrupa todos los datos operativos. |
| `Membership` | Une usuario, organización y rol. | Una por usuario y organización. |
| `Role` | Rol predefinido asignable a membresías. | Agrupa permisos. |
| `Permission` | Capacidad estable autorizable. | Se relaciona con roles mediante `RolePermission`. |
| `RolePermission` | Asociación entre un rol y una capacidad. | Tiene una clave compuesta rol–permiso. |
| `Invitation` | Invitación temporal para crear o incorporar una cuenta. | Pertenece a una organización y asigna un rol. |
| `RefreshSession` | Sesión renovable y revocable de un dispositivo. | Pertenece a un usuario. |

Una solicitud autenticada identifica primero al usuario. Para operar sobre datos de negocio también debe incluir `X-Organization-Id`; el servidor resuelve una membresía activa y sus permisos.

## Ubicaciones y catálogo

| Entidad | Responsabilidad | Relaciones principales |
| --- | --- | --- |
| `Branch` | Sucursal operativa de la organización. | Contiene almacenes. |
| `Warehouse` | Ubicación física que mantiene existencias. | Pertenece a una sucursal. |
| `Product` | Artículo identificado por SKU dentro de la organización. | Tiene saldos, movimientos y proveedores. |
| `Supplier` | Empresa que puede abastecer productos. | Se asocia con productos y entradas. |
| `ProductSupplier` | Relación muchos a muchos entre producto y proveedor. | No almacena precios en el MVP. |

## Inventario y operaciones

| Entidad | Responsabilidad | Relaciones principales |
| --- | --- | --- |
| `InventoryBalance` | Estado actual de un producto en un almacén. | Único por producto y almacén; contiene mínimo local. |
| `InventoryOperation` | Cabecera inmutable de un comando de inventario. | Contiene actor, tipo, motivo, fecha y movimientos. |
| `InventoryMovement` | Línea inmutable de cambio físico o reservado. | Referencia una operación y un saldo. |
| `InventoryEntry` | Datos específicos de una entrada. | Relaciona la operación con un proveedor opcional. |
| `Transfer` | Traslado atómico entre dos almacenes. | Produce movimientos de salida y entrada. |
| `OutboundOrder` | Solicitud de salida abastecida desde un único almacén. | Contiene uno o más renglones. |
| `OutboundOrderLine` | Producto y cantidad solicitada. | Producto único dentro de la orden. |
| `OutboundOrderOperation` | Relación entre una orden y las operaciones que reserva, libera o consume inventario. | Evita duplicar datos de la orden en el ledger. |
| `IdempotencyRecord` | Resultado durable de un comando crítico. | Único por organización y clave. |
| `AuditEvent` | Evidencia de una acción sensible. | Registra actor, entidad y cambios seguros. |
| `AuditChange` | Cambio de un campo auditado. | Pertenece a un evento y guarda valores redactados. |

## Estados y tipos

- Membresía: `ACTIVE`, `INACTIVE`.
- Invitación: `PENDING`, `ACCEPTED`, `REVOKED`, `EXPIRED`.
- Orden: `DRAFT`, `CONFIRMED`, `COMPLETED`, `CANCELLED`.
- Operación de inventario: `ENTRY`, `EXIT`, `ADJUSTMENT`, `TRANSFER`, `ORDER_RESERVE`, `ORDER_RELEASE`, `ORDER_FULFILL`.
- Roles predefinidos como datos: `OWNER`, `ADMIN`, `MANAGER`, `OPERATOR`, `VIEWER`.

## Identidad y ciclo de vida

Todos los identificadores públicos son UUID. Las entidades operativas guardan `createdAt` y, cuando son editables, `updatedAt`. Productos, proveedores, sucursales y almacenes se desactivan con `isActive`; no se eliminan si tienen historial.

Véase [[Reglas de Negocio]], [[Modelo Conceptual]] y [[../04 Base de Datos/Diccionario de Datos|Diccionario de datos]].
