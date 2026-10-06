# Reglas de Negocio

## Organizaciones y acceso

- **RN-001:** Toda entidad operativa pertenece directa o indirectamente a una organización.
- **RN-002:** Un usuario puede pertenecer a varias organizaciones, pero sólo una membresía se evalúa por solicitud.
- **RN-003:** La combinación usuario-organización es única y debe estar activa para operar.
- **RN-004:** Sólo el propietario puede modificar datos de la organización y no puede desactivarse si es el último propietario activo.
- **RN-005:** Una invitación sólo puede aceptarse una vez, por el correo invitado y antes de 72 horas.
- **RN-006:** Los permisos se obtienen de las relaciones `Role`–`Permission` del rol de la membresía; el cliente nunca concede permisos.

## Catálogo y ubicaciones

- **RN-007:** El SKU es obligatorio y único dentro de la organización, comparado sin distinguir mayúsculas.
- **RN-008:** Un almacén pertenece a una sucursal de la misma organización.
- **RN-009:** Un producto y un proveedor sólo pueden relacionarse dentro de la misma organización.
- **RN-010:** Un catálogo con historial se desactiva. Un recurso inactivo puede consultarse, pero no participar en operaciones nuevas.

## Invariantes de inventario

- **RN-011:** `onHand >= 0`, `reserved >= 0` y `reserved <= onHand`.
- **RN-012:** La disponibilidad se calcula como `onHand - reserved` y no se persiste.
- **RN-013:** Las cantidades operativas son enteros positivos. Sólo los deltas derivados pueden ser negativos.
- **RN-014:** El saldo es único por organización, almacén y producto.
- **RN-015:** El saldo se crea con ceros al configurar su mínimo o al ejecutar la primera operación válida para el producto y almacén.
- **RN-016:** Cada comando crea una operación y al menos un movimiento inmutable en la misma transacción que modifica sus saldos.
- **RN-017:** Un ajuste requiere motivo; entradas y salidas admiten referencia externa y las entradas pueden indicar proveedor.
- **RN-018:** Una salida o ajuste negativo no puede consumir unidades reservadas.
- **RN-019:** El mínimo es un entero no negativo configurado por producto y almacén. Hay alerta cuando `available <= minimumStock`.

## Concurrencia y atomicidad

- **RN-020:** Las operaciones críticas usan aislamiento `Serializable`; cada saldo se actualiza sólo si conserva los valores observados al validarlo.
- **RN-021:** Un conflicto Prisma `P2034` o una actualización condicional sin coincidencia reintenta la transacción completa hasta tres veces; si persiste, no produce cambios parciales.
- **RN-022:** Una transferencia exige almacenes distintos, activos y de la misma organización; origen, destino y movimientos cambian atómicamente.
- **RN-023:** Una clave idempotente repetida con la misma carga devuelve el resultado guardado; con otra carga responde conflicto.

## Órdenes

- **RN-024:** Una orden usa un solo almacén y contiene al menos un producto; no repite productos.
- **RN-025:** Sólo una orden `DRAFT` puede editar almacén, referencia, notas o renglones.
- **RN-026:** Confirmar valida todos los saldos dentro de una transacción serializable y reserva todos los renglones o ninguno.
- **RN-027:** Cancelar una orden `CONFIRMED` libera reservas sin cambiar existencia física.
- **RN-028:** Completar una orden `CONFIRMED` reduce `onHand` y `reserved` por la misma cantidad.
- **RN-029:** `COMPLETED` y `CANCELLED` son estados terminales.
- **RN-030:** Una orden `DRAFT` puede cancelarse sin afectar inventario.

## Auditoría

- **RN-031:** Cada mutación sensible exitosa registra un evento con actor, organización, acción, tipo e ID de entidad, fecha y `requestId`.
- **RN-032:** Cada campo modificado se registra como `AuditChange`; contraseñas, hashes, tokens, cookies y secretos se excluyen.
- **RN-033:** Movimientos y auditorías no se editan ni eliminan desde la API.

## Matriz de permisos

| Permiso | OWNER | ADMIN | MANAGER | OPERATOR | VIEWER |
| --- | :---: | :---: | :---: | :---: | :---: |
| `organization:manage` | Sí | No | No | No | No |
| `member:manage` | Sí | Sí | No | No | No |
| `catalog:read` | Sí | Sí | Sí | Sí | Sí |
| `catalog:write` | Sí | Sí | Sí | No | No |
| `inventory:read` | Sí | Sí | Sí | Sí | Sí |
| `inventory:write` | Sí | Sí | Sí | Sí | No |
| `order:write` | Sí | Sí | Sí | Sí | No |
| `audit:read` | Sí | Sí | Sí | No | No |
| `dashboard:read` | Sí | Sí | Sí | Sí | Sí |

