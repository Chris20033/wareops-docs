# Sprint 05 — Órdenes y Reservas

**Estado:** Pending  
**Objetivo:** completar el ciclo de una orden de salida abastecida desde un almacén.

## Dependencias

Sprint 03 completado; Sprint 04 recomendado para la secuencia de demostración.

## Backend

- [ ] Añadir los modelos Prisma `OutboundOrder`, `OutboundOrderLine` y `OutboundOrderOperation`.
- [ ] Generar número global único para una orden.
- [ ] Implementar creación de orden en estado `DRAFT`.
- [ ] Validar almacén de despacho activo al crear una orden.
- [ ] Validar que el creador pertenezca al tenant del almacén.
- [ ] Implementar listado paginado de órdenes.
- [ ] Implementar filtros de órdenes por estado.
- [ ] Implementar detalle de orden.
- [ ] Implementar actualización de encabezado de orden `DRAFT`.
- [ ] Implementar creación de renglón de orden.
- [ ] Validar cantidad positiva en un renglón.
- [ ] Validar que el producto pertenezca al tenant de la orden.
- [ ] Impedir productos repetidos en una orden.
- [ ] Implementar actualización de renglón de orden `DRAFT`.
- [ ] Implementar eliminación de renglón de orden `DRAFT`.
- [ ] Impedir edición de una orden no `DRAFT`.
- [ ] Implementar comando idempotente de confirmación.
- [ ] Validar que una orden tenga al menos un renglón antes de confirmar.
- [ ] Leer todos los saldos de renglones dentro de una transacción `Serializable`.
- [ ] Validar disponibilidad de todos los renglones antes de reservar.
- [ ] Aumentar `reserved` de cada saldo al confirmar.
- [ ] Crear operación `ORDER_RESERVE` al confirmar.
- [ ] Crear movimientos de reserva al confirmar.
- [ ] Crear relaciones `OutboundOrderOperation` de reserva.
- [ ] Cambiar estado a `CONFIRMED` sólo después de reservar todos los renglones.
- [ ] Implementar cancelación idempotente de borrador.
- [ ] Implementar cancelación idempotente de orden confirmada.
- [ ] Disminuir `reserved` de cada saldo al cancelar una orden confirmada.
- [ ] Crear operación `ORDER_RELEASE` al cancelar una orden confirmada.
- [ ] Crear movimientos de liberación al cancelar una orden confirmada.
- [ ] Cambiar estado a `CANCELLED`.
- [ ] Implementar finalización idempotente de orden confirmada.
- [ ] Disminuir `onHand` de cada saldo al finalizar.
- [ ] Disminuir `reserved` de cada saldo al finalizar.
- [ ] Crear operación `ORDER_FULFILL` al finalizar.
- [ ] Crear movimientos de salida al finalizar.
- [ ] Crear relaciones `OutboundOrderOperation` de finalización.
- [ ] Cambiar estado a `COMPLETED`.
- [ ] Crear auditoría para cada transición de orden.

## Frontend

- [ ] Crear listado de órdenes.
- [ ] Crear filtros de estado en el listado.
- [ ] Crear formulario de nueva orden.
- [ ] Crear selector de almacén de despacho.
- [ ] Crear editor de renglones de orden.
- [ ] Crear selector de producto por renglón.
- [ ] Crear campo de cantidad por renglón.
- [ ] Mostrar disponibilidad del producto en el almacén de la orden.
- [ ] Crear acción de editar encabezado de borrador.
- [ ] Crear acción de agregar renglón.
- [ ] Crear acción de editar renglón.
- [ ] Crear acción de eliminar renglón.
- [ ] Deshabilitar edición cuando la orden no sea `DRAFT`.
- [ ] Crear acción de confirmar orden.
- [ ] Mostrar resumen de reservas antes de confirmar.
- [ ] Crear acción de cancelar borrador.
- [ ] Crear acción de cancelar orden confirmada.
- [ ] Crear acción de finalizar orden confirmada.
- [ ] Solicitar confirmación visual antes de cancelar o finalizar.
- [ ] Generar `Idempotency-Key` para cada transición.
- [ ] Crear pantalla de detalle de orden.
- [ ] Mostrar historial de operaciones relacionadas en el detalle.

## Datos e Infraestructura

- [ ] Crear migración Prisma de órdenes y reservas.
- [ ] Añadir índices Prisma de estado, almacén, renglones y operaciones de orden.
- [ ] Crear datos seed de órdenes en borrador.
- [ ] Crear datos seed de órdenes confirmadas.
- [ ] Crear datos seed de órdenes completadas.
- [ ] Crear datos seed de órdenes canceladas.

## Documentación

- [ ] Documentar creación y listado de órdenes en OpenAPI.
- [ ] Documentar edición de borrador y renglones en OpenAPI.
- [ ] Documentar comando de confirmación en OpenAPI.
- [ ] Documentar comando de cancelación en OpenAPI.
- [ ] Documentar comando de finalización en OpenAPI.
- [ ] Documentar transiciones y errores de estado en OpenAPI.
- [ ] Actualizar la máquina de estados de orden.
- [ ] Actualizar la secuencia de reserva y finalización.

## Pruebas

- [ ] Probar que una orden requiere un almacén.
- [ ] Probar que una orden requiere al menos un renglón para confirmar.
- [ ] Probar que un renglón exige cantidad positiva.
- [ ] Probar que un producto no se repite en la orden.
- [ ] Probar que una orden no `DRAFT` no se edita.
- [ ] Probar que confirmar reserva todos los renglones.
- [ ] Probar que confirmar sin disponibilidad no reserva ningún renglón.
- [ ] Probar que una reserva reduce disponibilidad.
- [ ] Probar que cancelar borrador no cambia saldos.
- [ ] Probar que cancelar confirmada libera reservas sin modificar `onHand`.
- [ ] Probar que finalizar reduce `onHand` y `reserved` por la misma cantidad.
- [ ] Probar que estados `COMPLETED` y `CANCELLED` son terminales.
- [ ] Probar reintento idempotente de confirmación.
- [ ] Probar reintento idempotente de cancelación.
- [ ] Probar reintento idempotente de finalización.
- [ ] Probar concurrencia de dos confirmaciones sobre la misma disponibilidad.

**Trazabilidad:** RF-023–029; CA-010–015.

## Cierre del sprint

- [ ] El usuario puede crear, confirmar y completar o cancelar una orden, observando los cambios de disponibilidad y movimientos.
