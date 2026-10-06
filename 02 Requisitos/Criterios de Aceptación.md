# Criterios de Aceptación

## Aislamiento multiempresa

- **CA-001:** Dado un token de la organización A, cuando se solicita por ID un recurso de B, la API responde como recurso no encontrado o no accesible y no revela sus datos.
- **CA-002:** Los filtros, conteos y dashboard sólo consideran filas de la organización activa.
- **CA-003:** Una relación enviada entre recursos de organizaciones distintas es rechazada aunque ambos IDs existan.

## Inventario y concurrencia

- **CA-004:** Una entrada de 10 sobre una existencia de 5 produce existencia física 15 y un único movimiento de entrada.
- **CA-005:** Una salida de 6 sobre disponibilidad 5 responde conflicto y no modifica existencias, movimientos ni auditoría de éxito.
- **CA-006:** Dos solicitudes concurrentes de salida de 4 sobre disponibilidad 5 no pueden completarse ambas.
- **CA-007:** Una transferencia completada modifica origen y destino y crea sus dos movimientos en la misma transacción.
- **CA-008:** Si falla la actualización del destino, la transferencia no altera el origen.
- **CA-009:** Repetir una solicitud con la misma clave y la misma carga devuelve el resultado original sin duplicar efectos.

## Órdenes

- **CA-010:** Todos los renglones de una orden se abastecen desde el almacén asignado a la orden.
- **CA-011:** Confirmar una orden reserva todos sus renglones o ninguno.
- **CA-012:** Mientras una orden está confirmada, la cantidad reservada deja de estar disponible para otras salidas.
- **CA-013:** Cancelar una orden confirmada lleva sus reservas a cero y conserva la existencia física.
- **CA-014:** Completar una orden confirmada reduce existencia física y reservada en las cantidades de la orden.
- **CA-015:** Reintentar la finalización idempotente no genera una segunda salida.

## Autorización y auditoría

- **CA-016:** Un lector puede consultar inventario pero recibe prohibición al intentar modificarlo.
- **CA-017:** Un operador no puede consultar auditoría ni administrar miembros.
- **CA-018:** Una operación sensible exitosa crea un evento con actor, organización, acción, entidad, identificador y fecha.
- **CA-019:** Los campos secretos, hashes y tokens nunca aparecen en los cambios de auditoría.

## Experiencia y contrato

- **CA-020:** Los listados conservan filtros en la URL y permiten navegar entre páginas.
- **CA-021:** Los formularios muestran validaciones antes del envío y presentan los errores de API de manera comprensible.
- **CA-022:** Swagger documenta autenticación, parámetros, cuerpos, respuestas de éxito y errores comunes.
- **CA-023:** El recorrido crítico de login, entrada, transferencia y orden completada pasa en Playwright sobre el entorno de pruebas.
