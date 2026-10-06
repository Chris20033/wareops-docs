# ADR-001 — Monolito modular

**Estado:** Accepted  
**Fecha:** 2026-09-14

## Contexto

El MVP necesita límites de dominio, transacciones y despliegue demostrable, pero será mantenido por una sola persona y no necesita escalado independiente por módulo.

## Decisión

La API será un monolito modular NestJS. Identidad, organizaciones, catálogo, inventario, órdenes, auditoría y dashboard tendrán módulos explícitos dentro de un proceso y una base PostgreSQL.

## Consecuencias

- Transacciones entre inventario, órdenes y auditoría son directas.
- Menor costo de desarrollo, pruebas y despliegue.
- Los límites se sostienen mediante interfaces internas y propiedad de datos, no mediante red.
- Si un módulo exige escalado o ciclo de vida independiente en el futuro, podrá extraerse con evidencia previa.
