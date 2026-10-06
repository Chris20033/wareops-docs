# Sprint 03 — Núcleo de Inventario

**Estado:** Pending  
**Objetivo:** registrar saldos y operaciones básicas sin perder consistencia ni trazabilidad.

## Dependencias

Sprint 02 completado.

## Backend

- [ ] Añadir modelos Prisma `InventoryBalance`, `InventoryOperation`, `InventoryMovement` e `InventoryEntry`.
- [ ] Crear el saldo al configurar un mínimo por primera vez.
- [ ] Crear el saldo al registrar la primera entrada válida.
- [ ] Implementar listado paginado de saldos.
- [ ] Implementar detalle de saldo.
- [ ] Implementar actualización de `minimumStock`.
- [ ] Calcular `available` como `onHand - reserved` en el mapper.
- [ ] Implementar comando de entrada idempotente.
- [ ] Validar cantidad positiva en una entrada.
- [ ] Asociar proveedor opcional a una entrada.
- [ ] Crear operación `ENTRY` al registrar una entrada.
- [ ] Crear movimiento de entrada al registrar una entrada.
- [ ] Implementar comando de salida idempotente.
- [ ] Validar disponibilidad antes de una salida.
- [ ] Crear operación `EXIT` al registrar una salida.
- [ ] Crear movimiento de salida al registrar una salida.
- [ ] Implementar comando de ajuste idempotente.
- [ ] Exigir motivo en un ajuste.
- [ ] Validar que un ajuste negativo no consuma reservas.
- [ ] Crear operación `ADJUSTMENT` al registrar un ajuste.
- [ ] Crear movimiento de ajuste al registrar un ajuste.
- [ ] Implementar historial paginado de movimientos.
- [ ] Implementar filtros de movimientos por producto.
- [ ] Implementar filtros de movimientos por almacén.
- [ ] Implementar filtros de movimientos por tipo.
- [ ] Implementar filtros de movimientos por actor.
- [ ] Implementar filtros de movimientos por rango de fechas.
- [ ] Implementar creación y lectura de `IdempotencyRecord`.
- [ ] Rechazar reutilización de clave idempotente con carga distinta.
- [ ] Crear evento y cambios de auditoría para cada operación exitosa.
- [ ] Ejecutar comandos de inventario en transacción Prisma `Serializable`.
- [ ] Usar actualización condicional de saldos con valores observados.
- [ ] Reintentar conflictos `P2034` hasta tres veces.
- [ ] Devolver `409 CONCURRENT_MODIFICATION` tras agotar reintentos.

## Frontend

- [ ] Crear listado de inventario por producto y almacén.
- [ ] Mostrar existencia física, reservada y disponible.
- [ ] Crear formulario de configuración de mínimo.
- [ ] Crear formulario de entrada.
- [ ] Crear selector de proveedor en la entrada.
- [ ] Crear formulario de salida.
- [ ] Crear formulario de ajuste.
- [ ] Generar una `Idempotency-Key` por envío de operación.
- [ ] Mostrar errores de disponibilidad sin perder los datos del formulario.
- [ ] Crear listado de movimientos.
- [ ] Crear filtros de movimientos.
- [ ] Crear detalle de movimiento.

## Datos e Infraestructura

- [ ] Crear migración Prisma del núcleo de inventario.
- [ ] Añadir índices Prisma de saldos, operaciones y movimientos.
- [ ] Crear datos seed de saldos iniciales.
- [ ] Crear datos seed de entradas, salidas y ajustes.
- [ ] Preparar fixture de solicitudes concurrentes contra PostgreSQL real.

## Documentación

- [ ] Documentar saldos y mínimo de inventario en OpenAPI.
- [ ] Documentar comando de entrada en OpenAPI.
- [ ] Documentar comando de salida en OpenAPI.
- [ ] Documentar comando de ajuste en OpenAPI.
- [ ] Documentar historial y filtros de movimientos en OpenAPI.
- [ ] Documentar `Idempotency-Key` en los comandos críticos.
- [ ] Actualizar el flujo crítico de operación de inventario.

## Pruebas

- [ ] Probar que una entrada de 10 sobre 5 termina en 15.
- [ ] Probar que una entrada crea una operación y un movimiento.
- [ ] Probar que una salida sin disponibilidad responde `409`.
- [ ] Probar que una salida rechazada no cambia saldo, movimiento ni auditoría.
- [ ] Probar que un ajuste sin motivo se rechaza.
- [ ] Probar que un ajuste negativo respeta unidades reservadas.
- [ ] Probar dos salidas concurrentes sobre las mismas unidades.
- [ ] Probar reintento de conflicto `P2034`.
- [ ] Probar respuesta `409` al agotar reintentos.
- [ ] Probar repetición idempotente con misma carga.
- [ ] Probar conflicto idempotente con carga distinta.
- [ ] Probar que saldo, operación, movimiento, auditoría e idempotencia comparten transacción.

**Trazabilidad:** RF-013–017, RF-020–022; RNF-006–011, RNF-015; CA-004–006, CA-009.

## Cierre del sprint

- [ ] El inventario básico puede operarse desde web y todas sus invariantes se demuestran con integración concurrente sin consultas raw.
