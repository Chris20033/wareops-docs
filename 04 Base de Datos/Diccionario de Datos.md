# Diccionario de Datos

Convenciones: `String/uuid` corresponde a `uuid`; `DateTime/timestamptz` se persiste en UTC; los nombres entre paréntesis son restricciones Prisma. Todas las entidades mutables incluyen `createdAt` y `updatedAt` salvo indicación contraria.

## Identidad, organizaciones y RBAC

### `User` → `users`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK, `@default(uuid())`. |
| `email` | String/varchar(320) | No | `@unique`; se guarda en minúsculas. |
| `passwordHash` | String/text | No | Hash Argon2id, nunca se expone. |
| `displayName` | String/varchar(120) | No | Nombre visible. |
| `isActive` | Boolean | No | Default `true`. |
| `createdAt`, `updatedAt` | DateTime/timestamptz | No | Creación y modificación. |

### `Organization` → `organizations`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `name` | String/varchar(120) | No | Nombre comercial. |
| `slug` | String/varchar(80) | No | `@unique`; minúsculas. |
| `timezone` | String/varchar(64) | No | Default `UTC`, identificador IANA. |
| `createdAt`, `updatedAt` | DateTime/timestamptz | No | Creación y modificación. |

### `Role` → `roles`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `code` | String/varchar(30) | No | `@unique`: `OWNER`, `ADMIN`, `MANAGER`, `OPERATOR`, `VIEWER`. |
| `name` | String/varchar(80) | No | Nombre visible. |
| `description` | String/text | Sí | Descripción funcional. |

### `Permission` → `permissions`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `code` | String/varchar(80) | No | `@unique`, por ejemplo `inventory:write`. |
| `description` | String/text | No | Conducta autorizada. |

### `RolePermission` → `role_permissions`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `roleId` | String/uuid | No | PK compuesta y FK a `Role`. |
| `permissionId` | String/uuid | No | PK compuesta y FK a `Permission`. |

### `Membership` → `memberships`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `userId` | String/uuid | No | FK a `User`. |
| `organizationId` | String/uuid | No | FK a `Organization`. |
| `roleId` | String/uuid | No | FK a `Role`. |
| `status` | `MembershipStatus` | No | `ACTIVE` o `INACTIVE`. |
| `createdAt`, `updatedAt` | DateTime/timestamptz | No | `@@unique([userId, organizationId])`. |

### `Invitation` → `invitations`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `organizationId` | String/uuid | No | FK a `Organization`. |
| `invitedByUserId` | String/uuid | No | FK a `User`; no determina el tenant. |
| `roleId` | String/uuid | No | FK a `Role`; `OWNER` se rechaza en dominio. |
| `email` | String/varchar(320) | No | Se guarda en minúsculas. |
| `tokenHash` | String/text | No | `@unique`. |
| `status` | `InvitationStatus` | No | `PENDING`, `ACCEPTED`, `REVOKED`, `EXPIRED`. |
| `expiresAt` | DateTime/timestamptz | No | Emisión + 72 horas. |
| `acceptedAt`, `revokedAt` | DateTime/timestamptz | Sí | Según transición. |
| `createdAt` | DateTime/timestamptz | No | Fecha de emisión. |

### `RefreshSession` → `refresh_sessions`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `userId` | String/uuid | No | FK a `User`. |
| `tokenHash` | String/text | No | `@unique`. |
| `expiresAt`, `lastUsedAt` | DateTime/timestamptz | No | Vencimiento y último uso. |
| `revokedAt` | DateTime/timestamptz | Sí | Revocación o cierre. |
| `userAgent`, `ipAddress` | String/text | Sí | Metadatos operativos. |
| `createdAt` | DateTime/timestamptz | No | Inicio de sesión. |

## Ubicaciones y catálogo

### `Branch` → `branches`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `organizationId` | String/uuid | No | FK a `Organization`. |
| `code` | String/varchar(40) | No | `@@unique([organizationId, code])`, mayúsculas. |
| `name` | String/varchar(120) | No | Nombre visible. |
| `address` | String/text | Sí | Dirección descriptiva no estructurada. |
| `isActive` | Boolean | No | Default `true`. |
| `createdAt`, `updatedAt` | DateTime/timestamptz | No | Creación y modificación. |

### `Warehouse` → `warehouses`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `branchId` | String/uuid | No | FK a `Branch`; determina organización. |
| `code` | String/varchar(40) | No | `@@unique([branchId, code])`, mayúsculas. |
| `name` | String/varchar(120) | No | Nombre visible. |
| `description` | String/text | Sí | Información operativa. |
| `isActive` | Boolean | No | Default `true`. |
| `createdAt`, `updatedAt` | DateTime/timestamptz | No | Creación y modificación. |

### `Product` → `products`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `organizationId` | String/uuid | No | FK a `Organization`. |
| `sku` | String/varchar(80) | No | `@@unique([organizationId, sku])`, mayúsculas. |
| `name` | String/varchar(160) | No | Nombre visible. |
| `description` | String/text | Sí | Descripción. |
| `isActive` | Boolean | No | Default `true`. |
| `createdAt`, `updatedAt` | DateTime/timestamptz | No | Creación y modificación. |

### `Supplier` → `suppliers`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `organizationId` | String/uuid | No | FK a `Organization`. |
| `code` | String/varchar(40) | No | `@@unique([organizationId, code])`, mayúsculas. |
| `name` | String/varchar(160) | No | Nombre visible. |
| `contactName` | String/varchar(120) | Sí | Contacto. |
| `email` | String/varchar(320) | Sí | Correo en minúsculas. |
| `phone` | String/varchar(40) | Sí | Teléfono. |
| `isActive` | Boolean | No | Default `true`. |
| `createdAt`, `updatedAt` | DateTime/timestamptz | No | Creación y modificación. |

### `ProductSupplier` → `product_suppliers`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `productId` | String/uuid | No | PK compuesta y FK a `Product`. |
| `supplierId` | String/uuid | No | PK compuesta y FK a `Supplier`. |
| `createdAt` | DateTime/timestamptz | No | Alta de relación. |

## Inventario

### `InventoryBalance` → `inventory_balances`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `warehouseId` | String/uuid | No | FK a `Warehouse`. |
| `productId` | String/uuid | No | FK a `Product`. |
| `onHand` | Int/integer | No | Default 0; dominio exige `>= 0`. |
| `reserved` | Int/integer | No | Default 0; dominio exige `0..onHand`. |
| `minimumStock` | Int/integer | No | Default 0; dominio exige `>= 0`. |
| `createdAt`, `updatedAt` | DateTime/timestamptz | No | `@@unique([warehouseId, productId])`. |

### `InventoryOperation` → `inventory_operations`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK y ID público de operación. |
| `actorMembershipId` | String/uuid | No | FK a `Membership`; determina actor y tenant. |
| `type` | `InventoryOperationType` | No | Entrada, salida, ajuste, transferencia o transición de orden. |
| `reason` | String/varchar(240) | Sí | Obligatorio según tipo. |
| `externalReference` | String/varchar(120) | Sí | Referencia del usuario. |
| `createdAt` | DateTime/timestamptz | No | Fecha inmutable. |

### `InventoryMovement` → `inventory_movements`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `operationId` | String/uuid | No | FK a `InventoryOperation`. |
| `balanceId` | String/uuid | No | FK a `InventoryBalance`. |
| `onHandDelta` | Int/integer | No | Cambio físico; puede ser cero. |
| `reservedDelta` | Int/integer | No | Cambio reservado; puede ser cero. |

Ambos deltas no pueden ser cero simultáneamente; esta regla se valida en dominio.

### `InventoryEntry` → `inventory_entries`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `operationId` | String/uuid | No | PK y FK a operación de tipo `ENTRY`. |
| `supplierId` | String/uuid | Sí | FK a `Supplier`. |

### `Transfer` → `transfers`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK e ID público de transferencia. |
| `operationId` | String/uuid | No | FK única a operación `TRANSFER`. |
| `sourceBalanceId` | String/uuid | No | FK al saldo origen. |
| `destinationBalanceId` | String/uuid | No | FK al saldo destino. |
| `quantity` | Int/integer | No | Entero positivo. |

Origen y destino deben ser distintos y corresponder al mismo producto y tenant.

## Órdenes

### `OutboundOrder` → `outbound_orders`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `warehouseId` | String/uuid | No | FK al único almacén de despacho. |
| `number` | String/varchar(40) | No | `@unique` global, generado por la aplicación. |
| `status` | `OutboundOrderStatus` | No | `DRAFT`, `CONFIRMED`, `COMPLETED`, `CANCELLED`. |
| `externalReference` | String/varchar(120) | Sí | Referencia externa. |
| `notes` | String/text | Sí | Notas operativas. |
| `createdByMembershipId` | String/uuid | No | FK a `Membership`; debe coincidir con tenant del almacén. |
| `confirmedAt`, `completedAt`, `cancelledAt` | DateTime/timestamptz | Sí | Según transición. |
| `createdAt`, `updatedAt` | DateTime/timestamptz | No | Creación y modificación. |

### `OutboundOrderLine` → `outbound_order_lines`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `orderId` | String/uuid | No | FK a `OutboundOrder`. |
| `productId` | String/uuid | No | FK a `Product`. |
| `quantity` | Int/integer | No | Entero positivo. |
| `createdAt`, `updatedAt` | DateTime/timestamptz | No | `@@unique([orderId, productId])`. |

### `OutboundOrderOperation` → `outbound_order_operations`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `orderId` | String/uuid | No | PK compuesta y FK a `OutboundOrder`. |
| `operationId` | String/uuid | No | PK compuesta, `@unique` y FK a `InventoryOperation`. |

## Plataforma

### `IdempotencyRecord` → `idempotency_records`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `organizationId` | String/uuid | No | FK a `Organization`. |
| `key` | String/varchar(128) | No | `@@unique([organizationId, key])`. |
| `requestHash` | String/char(64) | No | Hash de método, ruta, tenant y cuerpo canónico. |
| `method`, `route` | String | No | Comando protegido. |
| `responseStatus` | Int/integer | No | Status reproducible. |
| `responseBody` | Json/jsonb | No | Resultado técnico opaco. |
| `resourceType`, `resourceId` | String | Sí | Referencia informativa. |
| `createdAt`, `expiresAt` | DateTime/timestamptz | No/Sí | Creación y retención opcional. |

### `AuditEvent` → `audit_events`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `organizationId` | String/uuid | No | FK a `Organization`. |
| `actorUserId` | String/uuid | Sí | FK a `User`; nulo para eventos del sistema. |
| `action`, `entityType` | String/varchar(80) | No | Acción y clase de entidad. |
| `entityId` | String/uuid | Sí | ID lógico; no es FK polimórfica. |
| `requestId` | String/uuid | No | Correlación con logs. |
| `createdAt` | DateTime/timestamptz | No | Fecha inmutable. |

### `AuditChange` → `audit_changes`

| Campo | Tipo | Nulo | Clave / regla |
| --- | --- | :---: | --- |
| `id` | String/uuid | No | PK. |
| `auditEventId` | String/uuid | No | FK a `AuditEvent`. |
| `field` | String/varchar(120) | No | `@@unique([auditEventId, field])`. |
| `oldValue`, `newValue` | String/text | Sí | Valor escalar serializado y redactado. |

## Enums

`MembershipStatus`, `InvitationStatus`, `OutboundOrderStatus` e `InventoryOperationType` son enums Prisma. Roles y permisos son datos relacionales predefinidos, no enums.

## Índices y claves compuestas Prisma

| Modelo | Declaraciones previstas |
| --- | --- |
| `User` | `email @unique`, `@@index([isActive])` |
| `Organization` | `slug @unique` |
| `Role`, `Permission` | `code @unique` |
| `RolePermission` | `@@id([roleId, permissionId])`, `@@index([permissionId])` |
| `Membership` | `@@unique([userId, organizationId])`, `@@index([userId, status])`, `@@index([organizationId, status, roleId])` |
| `Invitation` | `tokenHash @unique`, `@@index([organizationId, status, createdAt])`, `@@index([email, status])`, `@@index([expiresAt])` |
| `RefreshSession` | `tokenHash @unique`, `@@index([userId, revokedAt])`, `@@index([expiresAt])` |
| `Branch` | `@@unique([organizationId, code])`, `@@index([organizationId, isActive, name])` |
| `Warehouse` | `@@unique([branchId, code])`, `@@index([branchId, isActive, name])` |
| `Product` | `@@unique([organizationId, sku])`, `@@index([organizationId, isActive, name])` |
| `Supplier` | `@@unique([organizationId, code])`, `@@index([organizationId, isActive, name])` |
| `ProductSupplier` | `@@id([productId, supplierId])`, `@@index([supplierId])` |
| `InventoryBalance` | `@@unique([warehouseId, productId])`, `@@index([productId])`, `@@index([warehouseId])` |
| `InventoryOperation` | `@@index([actorMembershipId, createdAt])`, `@@index([type, createdAt])` |
| `InventoryMovement` | `@@unique([operationId, balanceId])`, `@@index([balanceId, id])` |
| `InventoryEntry` | `operationId @id`, `@@index([supplierId])` |
| `Transfer` | `operationId @unique`, `@@index([sourceBalanceId])`, `@@index([destinationBalanceId])` |
| `OutboundOrder` | `number @unique`, `@@index([warehouseId, status, createdAt])`, `@@index([createdByMembershipId])` |
| `OutboundOrderLine` | `@@unique([orderId, productId])`, `@@index([productId])` |
| `OutboundOrderOperation` | `@@id([orderId, operationId])`, `operationId @unique` |
| `IdempotencyRecord` | `@@unique([organizationId, key])`, `@@index([organizationId, createdAt])`, `@@index([expiresAt])` |
| `AuditEvent` | `@@index([organizationId, createdAt])`, `@@index([organizationId, action])`, `@@index([actorUserId])`, `@@index([entityType, entityId])` |
| `AuditChange` | `@@unique([auditEventId, field])` |
