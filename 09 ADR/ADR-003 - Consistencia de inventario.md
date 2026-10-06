# ADR-003 — Consistencia de inventario

**Estado:** Accepted  
**Fecha:** 2026-09-14

## Contexto

Salidas, transferencias y reservas concurrentes pueden observar la misma disponibilidad y consumirla dos veces. El proyecto, además, establece Prisma como única capa de datos.

## Decisión

Cada comando crítico se ejecutará en una transacción interactiva Prisma con aislamiento `Serializable`. Después de leer y validar los saldos, `updateMany` exigirá que `onHand` y `reserved` todavía coincidan con los valores observados antes de aplicar incrementos o decrementos.

Los conflictos de escritura o serialización `P2034`, así como una actualización condicional que afecte cero filas, reintentarán la transacción completa hasta tres veces. Un cuarto conflicto se responderá como `409 CONCURRENT_MODIFICATION` sin efectos parciales.

## Consecuencias

- No se escriben bloqueos ni consultas SQL manuales.
- Transferencias y órdenes conservan semántica todo-o-nada.
- Los servicios deben ser deterministas y no ejecutar llamadas externas dentro de la transacción.
- Se requieren pruebas concurrentes con PostgreSQL real para verificar el comportamiento, no sólo mocks.
