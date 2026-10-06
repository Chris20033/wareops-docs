# Estado del MVP

> [!info] Estado global: **In Progress**
> La fundación de API y web está lista; el backend de identidad, multi-tenancy y RBAC (Sprint 01) se encuentra implementado.

| Capacidad | Estado | Sprint |
| --- | --- | --- |
| Fundación, CI y entorno local | In Progress | [[Sprint 00 - Fundación]] |
| Identidad, organizaciones y RBAC | Completed | [[Sprint 01 - Identidad y Multi-tenancy]] |
| Ubicaciones y catálogo | In Progress | [[Sprint 02 - Ubicaciones y Catálogo]] |
| Saldos y movimientos | Pending | [[Sprint 03 - Núcleo de Inventario]] |
| Transferencias | Pending | [[Sprint 04 - Transferencias]] |
| Órdenes y reservas | Pending | [[Sprint 05 - Órdenes y Reservas]] |
| Dashboard y auditoría | Pending | [[Sprint 06 - Supervisión]] |
| Calidad, despliegue y demo | Pending | [[Sprint 07 - Cierre de Portafolio]] |

## Definición de MVP completo

- Todas las capacidades obligatorias están `Completed`.
- Lint, pruebas y build pasan en CI en API y web.
- Las pruebas de aislamiento, autorización, concurrencia e idempotencia pasan contra PostgreSQL.
- El recorrido Playwright de demostración pasa en un entorno desplegado.
- OpenAPI, migraciones, seed, README y este vault coinciden con el comportamiento implementado.

Los estados permitidos son `Pending`, `In Progress`, `Completed` y `Deferred`. Sólo se actualizan con evidencia ejecutable o una decisión explícita de alcance.
