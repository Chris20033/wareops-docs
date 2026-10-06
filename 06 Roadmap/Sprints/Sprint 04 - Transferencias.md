# Sprint 04 — Transferencias

**Estado:** Pending  
**Objetivo:** trasladar inventario entre almacenes sin estados parciales.

## Dependencias

Sprint 03 completado.

## Backend

- [ ] Añadir el modelo Prisma `Transfer`.
- [ ] Implementar el endpoint de creación de transferencia.
- [ ] Validar que el almacén origen exista y esté activo.
- [ ] Validar que el almacén destino exista y esté activo.
- [ ] Validar que origen y destino sean distintos.
- [ ] Validar que origen y destino pertenezcan al mismo tenant.
- [ ] Validar que ambos saldos correspondan al mismo producto.
- [ ] Validar cantidad positiva.
- [ ] Validar disponibilidad suficiente en el saldo origen.
- [ ] Crear una operación `TRANSFER`.
- [ ] Crear el registro `Transfer`.
- [ ] Reducir `onHand` del saldo origen.
- [ ] Aumentar `onHand` del saldo destino.
- [ ] Crear movimiento negativo para el origen.
- [ ] Crear movimiento positivo para el destino.
- [ ] Crear evento y cambios de auditoría de transferencia.
- [ ] Ejecutar la transferencia en una transacción Prisma `Serializable`.
- [ ] Aplicar actualización condicional al saldo origen.
- [ ] Aplicar actualización condicional al saldo destino.
- [ ] Reintentar conflictos de transferencia hasta tres veces.
- [ ] Implementar idempotencia de transferencia.
- [ ] Implementar detalle de transferencia.
- [ ] Incluir ambos movimientos en el detalle de transferencia.

## Frontend

- [ ] Crear página de transferencia.
- [ ] Crear selector de almacén origen.
- [ ] Crear selector de almacén destino.
- [ ] Crear selector de producto.
- [ ] Mostrar disponibilidad del almacén origen.
- [ ] Crear campo de cantidad.
- [ ] Crear campo de motivo.
- [ ] Crear campo de referencia opcional.
- [ ] Validar que origen y destino sean distintos antes del envío.
- [ ] Generar `Idempotency-Key` al enviar la transferencia.
- [ ] Mostrar resumen de transferencia antes de confirmar.
- [ ] Mostrar error de disponibilidad insuficiente.
- [ ] Crear pantalla de detalle de transferencia.
- [ ] Mostrar movimientos de origen y destino en el detalle.

## Datos e Infraestructura

- [ ] Crear migración Prisma de transferencias.
- [ ] Añadir índices Prisma para saldo origen y saldo destino.
- [ ] Crear datos seed de transferencias demostrables.
- [ ] Preparar fixture que fuerce un fallo dentro de una transferencia.

## Documentación

- [ ] Documentar el comando de transferencia en OpenAPI.
- [ ] Documentar errores de origen y destino inválidos.
- [ ] Documentar error de disponibilidad insuficiente.
- [ ] Documentar detalle de transferencia en OpenAPI.
- [ ] Actualizar el diagrama de secuencia de transferencia.

## Pruebas

- [ ] Probar rechazo cuando origen y destino son el mismo almacén.
- [ ] Probar rechazo de almacén inactivo.
- [ ] Probar rechazo de almacenes de organizaciones distintas.
- [ ] Probar rechazo de saldos de productos distintos.
- [ ] Probar rechazo por disponibilidad insuficiente.
- [ ] Probar que origen disminuye exactamente la cantidad transferida.
- [ ] Probar que destino aumenta exactamente la cantidad transferida.
- [ ] Probar que la transferencia crea dos movimientos.
- [ ] Probar que un fallo revierte origen, destino, movimientos y auditoría.
- [ ] Probar reintento por conflicto serializable.
- [ ] Probar repetición idempotente de transferencia.

**Trazabilidad:** RF-018–019, RF-021–022; CA-007–009.

## Cierre del sprint

- [ ] La demostración permite transferir unidades y navegar desde la transferencia hacia ambos movimientos.
