# Errores de API

## Formato

```json
{
  "statusCode": 409,
  "code": "INSUFFICIENT_STOCK",
  "message": "No hay existencia disponible suficiente.",
  "details": { "available": 5, "requested": 6 },
  "requestId": "uuid"
}
```

`details` es opcional y sólo contiene datos seguros y accionables. En validación puede incluir `fields`, un mapa de propiedad a códigos/mensajes. Stack traces, SQL, hashes, tokens y configuraciones nunca se exponen.

Todas las respuestas de error incluyen `X-Request-Id` con el mismo UUID de `requestId`. Una cabecera `X-Request-Id` inválida usa `details.fields.X-Request-Id = ["INVALID_UUID"]` y no refleja el valor rechazado.

## Códigos comunes

| HTTP | Código | Uso |
| ---: | --- | --- |
| 400 | `VALIDATION_ERROR` | Forma, tipos o valores inválidos. |
| 401 | `AUTHENTICATION_REQUIRED` | Access token ausente, inválido o expirado. |
| 401 | `INVALID_CREDENTIALS` | Login rechazado sin revelar qué dato falló. |
| 401 | `REFRESH_SESSION_INVALID` | Refresh expirado, revocado o reutilizado. |
| 403 | `PERMISSION_DENIED` | Membresía válida sin capacidad requerida. |
| 404 | `RESOURCE_NOT_FOUND` | Recurso inexistente o fuera del tenant. |
| 409 | `DUPLICATE_RESOURCE` | SKU, código o relación ya existente. |
| 409 | `INSUFFICIENT_STOCK` | Disponibilidad menor a la solicitada. |
| 409 | `INVALID_STATE_TRANSITION` | Estado incompatible con el comando. |
| 409 | `IDEMPOTENCY_KEY_REUSED` | Misma clave con una carga distinta. |
| 409 | `CONCURRENT_MODIFICATION` | Conflicto transitorio no resuelto. |
| 422 | `BUSINESS_RULE_VIOLATION` | Regla de dominio que no encaja en otro código. |
| 429 | `RATE_LIMITED` | Reservado para la incorporación futura de límites. |
| 500 | `INTERNAL_ERROR` | Error inesperado con `requestId`. |
| 503 | `DEPENDENCY_UNAVAILABLE` | Dependencia esencial no disponible. |

## Política de reintentos

El cliente no reintenta mutaciones automáticamente salvo renovación de sesión antes de enviarlas. Una operación crítica puede reenviarse deliberadamente con la misma `Idempotency-Key`. Lecturas pueden reintentarse con backoff limitado ante fallos transitorios.
