# Convenciones de API

## Base y transporte

- Base URL: `/api/v1`.
- JSON UTF-8 y fechas ISO 8601 en UTC.
- Bearer access token en endpoints protegidos.
- `X-Organization-Id` UUID obligatorio en endpoints de negocio.
- `Idempotency-Key` de 1–128 caracteres obligatorio en comandos críticos.
- `X-Request-Id` UUID opcional; si falta, la API lo genera y siempre lo devuelve tanto en el cuerpo como en la cabecera de respuesta. Si la cabecera está presente pero no es un UUID válido, responde `400 VALIDATION_ERROR` y genera un nuevo `requestId` para correlacionar el rechazo.

## Respuestas

Recurso único:

```json
{ "data": { "id": "uuid" }, "requestId": "uuid" }
```

Colección:

```json
{
  "data": [],
  "meta": { "page": 1, "pageSize": 20, "totalItems": 0, "totalPages": 0 },
  "requestId": "uuid"
}
```

Creación devuelve `201`; lectura y comandos exitosos `200`; actualización parcial `200`; operaciones sin cuerpo `204` sólo cuando no se necesita representar el nuevo estado.

## Listados

- `page` inicia en 1; `pageSize` por defecto 20 y máximo 100.
- `search` realiza búsqueda textual acotada al recurso.
- `sort` acepta únicamente campos publicados; `order` es `asc` o `desc`.
- Filtros usan nombres explícitos como `warehouseId`, `status`, `from` y `to`.
- Orden por defecto estable: `createdAt desc, id desc`, salvo catálogos por `name asc, id asc`.

## Escrituras

- `POST` crea recursos o ejecuta comandos; `PATCH` modifica parcialmente; no se usa `PUT` en el MVP.
- Catálogos se desactivan con `PATCH { "isActive": false }`; no existen endpoints destructivos.
- Comandos críticos: entradas, salidas, ajustes, transferencias, confirmar/cancelar/completar órdenes y aceptar invitaciones.
- El hash idempotente canoniza método, ruta, tenant y cuerpo. Repetir misma clave/carga devuelve el status y cuerpo originales; cambiar la carga devuelve `409 IDEMPOTENCY_KEY_REUSED`.

## Nombres y validación

- Propiedades JSON en `camelCase`; enums en `UPPER_SNAKE_CASE`.
- IDs inválidos responden `400`; recurso ajeno o inexistente responde `404` cuando corresponda proteger existencia.
- Propiedades desconocidas se rechazan.
- Cantidades son enteros positivos; mínimos aceptan cero.

Véase [[Errores]] y [[Catálogo de Endpoints]].
