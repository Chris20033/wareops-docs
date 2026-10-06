# Catálogo de Endpoints

Todos los endpoints salvo registro, login, refresh, aceptación de invitación y salud requieren bearer token. Los endpoints marcados como **tenant** requieren además `X-Organization-Id`.

## Autenticación y organizaciones

| Método | Ruta | Permiso / comportamiento |
| --- | --- | --- |
| POST | `/auth/register` | Crea usuario, organización y membresía `OWNER`. |
| POST | `/auth/login` | Devuelve access token y cookie refresh. |
| POST | `/auth/refresh` | Rota refresh y devuelve access token. |
| POST | `/auth/logout` | Revoca sesión actual. |
| GET | `/auth/me` | Perfil, sesión y organizaciones accesibles. |
| GET | `/organizations` | Organizaciones del usuario. |
| GET | `/organizations/current` | **tenant**, detalle de la organización activa. |
| PATCH | `/organizations/current` | **tenant**, `organization:manage`. |
| GET | `/members` | **tenant**, `member:manage`. |
| PATCH | `/members/{membershipId}` | **tenant**, cambia rol/estado según reglas. |
| POST | `/invitations` | **tenant**, crea invitación y devuelve enlace una vez. |
| GET | `/invitations` | **tenant**, lista invitaciones. |
| POST | `/invitations/{invitationId}/revoke` | **tenant**, revoca invitación pendiente. |
| POST | `/invitations/accept` | Token idempotente; crea o activa membresía. |

Al aceptar una invitación, una cuenta autenticada debe tener el mismo correo. Si todavía no existe cuenta, la solicitud incluye `displayName` y `password`; el correo se obtiene del token y no puede sustituirse en el cuerpo.

## Sucursales y almacenes

| Método | Ruta | Permiso |
| --- | --- | --- |
| GET, POST | `/branches` | **tenant**, `catalog:read` / `catalog:write`. |
| GET, PATCH | `/branches/{branchId}` | **tenant**, lectura / escritura de catálogo. |
| GET, POST | `/warehouses` | **tenant**, lectura / escritura de catálogo. |
| GET, PATCH | `/warehouses/{warehouseId}` | **tenant**, lectura / escritura de catálogo. |

## Productos y proveedores

| Método | Ruta | Permiso |
| --- | --- | --- |
| GET, POST | `/products` | **tenant**, `catalog:read` / `catalog:write`. |
| GET, PATCH | `/products/{productId}` | **tenant**, lectura / escritura de catálogo. |
| GET, POST | `/suppliers` | **tenant**, lectura / escritura de catálogo. |
| GET, PATCH | `/suppliers/{supplierId}` | **tenant**, lectura / escritura de catálogo. |
| GET, POST | `/products/{productId}/suppliers` | **tenant**, lista o asocia proveedores. |
| DELETE | `/products/{productId}/suppliers/{supplierId}` | **tenant**, elimina sólo la relación sin historial operativo. |

## Inventario y movimientos

| Método | Ruta | Permiso / cuerpo esencial |
| --- | --- | --- |
| GET | `/inventory` | **tenant**, `inventory:read`; filtra producto/almacén/alerta. |
| GET | `/inventory/{balanceId}` | **tenant**, `inventory:read`. |
| PATCH | `/inventory/{balanceId}/minimum-stock` | **tenant**, `catalog:write`; `{ minimumStock }`. |
| POST | `/inventory/entries` | **tenant**, `inventory:write`, idempotente; producto, almacén, cantidad, proveedor?, motivo?, referencia?. |
| POST | `/inventory/exits` | **tenant**, `inventory:write`, idempotente; producto, almacén, cantidad, motivo, referencia?. |
| POST | `/inventory/adjustments` | **tenant**, `inventory:write`, idempotente; producto, almacén, delta distinto de cero, motivo. |
| POST | `/inventory/transfers` | **tenant**, `inventory:write`, idempotente; producto, origen, destino, cantidad, motivo. |
| GET | `/inventory/transfers/{transferId}` | **tenant**, `inventory:read`. |
| GET | `/movements` | **tenant**, `inventory:read`; filtros por fecha, tipo, producto, almacén, actor y operación. |
| GET | `/movements/{movementId}` | **tenant**, `inventory:read`. |

## Órdenes de salida

| Método | Ruta | Permiso / comportamiento |
| --- | --- | --- |
| GET, POST | `/outbound-orders` | **tenant**, lectura / `order:write`; crea borrador con almacén y renglones. |
| GET, PATCH | `/outbound-orders/{orderId}` | **tenant**, consulta o edita sólo `DRAFT`. |
| POST | `/outbound-orders/{orderId}/confirm` | **tenant**, idempotente; reserva toda la orden. |
| POST | `/outbound-orders/{orderId}/cancel` | **tenant**, idempotente; libera reservas si aplica. |
| POST | `/outbound-orders/{orderId}/complete` | **tenant**, idempotente; consume existencia reservada. |

## Supervisión

| Método | Ruta | Permiso |
| --- | --- | --- |
| GET | `/dashboard/summary` | **tenant**, `dashboard:read`. |
| GET | `/dashboard/low-stock` | **tenant**, `dashboard:read`. |
| GET | `/dashboard/recent-movements` | **tenant**, `dashboard:read`. |
| GET | `/audit-events` | **tenant**, `audit:read`. |
| GET | `/audit-events/{eventId}` | **tenant**, `audit:read`. |

El detalle de auditoría devuelve `changes` como una colección de `{ field, oldValue, newValue }`; nunca expone contraseñas, hashes, tokens ni cookies.

## Operación

| Método | Ruta | Acceso |
| --- | --- | --- |
| GET | `/health/live` | Público, sin detalles sensibles. |
| GET | `/health/ready` | Público, estado agregado de dependencias. |
| GET | `/docs` | Configurable; público en demo, restringible en otros entornos. |

Contratos de salud de la fundación:

```json
{
  "data": { "status": "ok" },
  "requestId": "uuid"
}
```

`GET /health/ready` añade `"dependencies": { "postgres": "up" }` dentro de `data`. Si PostgreSQL no acepta la conexión, responde `503 DEPENDENCY_UNAVAILABLE` con `details: { "postgres": "down" }`. Liveness no consulta la base de datos. El documento OpenAPI serializado está disponible en `/docs-json`.

Los DTO, ejemplos y respuestas exactas se mantendrán en OpenAPI; este documento es el catálogo funcional estable.
