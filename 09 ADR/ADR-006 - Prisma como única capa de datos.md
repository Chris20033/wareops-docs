# ADR-006 — Prisma como única capa de datos

**Estado:** Accepted  
**Fecha:** 2026-09-14

## Contexto

WareOps busca demostrar un backend mantenible por una sola persona. Mezclar Prisma con SQL manual duplicaría convenciones, tipos y caminos de acceso, y dificultaría que el esquema documentado fuera la fuente de verdad.

## Decisión

La API accederá a PostgreSQL exclusivamente mediante Prisma Client. `schema.prisma` definirá el modelo en 3FN, relaciones, enums, índices y restricciones compatibles. Prisma Migrate generará las migraciones sin edición manual.

Las lecturas usarán `select`, `include`, filtros relacionales y agregaciones. Las escrituras críticas usarán transacciones Prisma `Serializable`, comparación de saldos y reintentos acotados.

## Consecuencias

- No se permiten `$queryRaw`, `$executeRaw`, TypedSQL, vistas, funciones, triggers ni procedimientos.
- Los DTO se construyen con selectores y mappers tipados.
- Las reglas no expresables en Prisma se validan en dominio y se prueban contra PostgreSQL real.
- Una optimización que requiera SQL necesita medición, cambio explícito de alcance y un ADR que reemplace esta decisión.
