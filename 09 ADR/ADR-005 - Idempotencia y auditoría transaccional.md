# ADR-005 — Idempotencia y auditoría transaccional

**Estado:** Accepted  
**Fecha:** 2026-09-14

## Contexto

Reintentos de red pueden duplicar movimientos. Guardar auditoría o resultados después de confirmar el negocio puede dejar operaciones sin evidencia o sin respuesta reproducible.

## Decisión

Los comandos críticos exigen `Idempotency-Key` única por organización. Se compara un hash canónico de la solicitud y el resultado exitoso se guarda junto con saldos, movimientos y auditoría en la misma transacción.

## Consecuencias

- Un reintento idéntico devuelve el resultado original sin repetir efectos.
- Reutilizar la clave con otra carga devuelve conflicto.
- La restricción única resuelve carreras entre solicitudes con la misma clave.
- La retención y limpieza de registros puede definirse después del MVP sin cambiar el contrato.
