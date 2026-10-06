# Registro de Decisiones de Arquitectura

| ADR | Estado | Decisión |
| --- | --- | --- |
| [[ADR-001 - Monolito modular|ADR-001]] | Accepted | API como monolito modular NestJS. |
| [[ADR-002 - Contexto multiempresa|ADR-002]] | Accepted | Tenant explícito y validado por membresía. |
| [[ADR-003 - Consistencia de inventario|ADR-003]] | Accepted | Transacciones Prisma serializables con comparación y reintento. |
| [[ADR-004 - Sesiones con refresh rotatorio|ADR-004]] | Accepted | Access en memoria y refresh opaco en cookie. |
| [[ADR-005 - Idempotencia y auditoría transaccional|ADR-005]] | Accepted | Resultado idempotente y evidencia en la transacción de negocio. |
| [[ADR-006 - Prisma como única capa de datos|ADR-006]] | Accepted | Modelo 3FN y acceso exclusivo mediante Prisma Client. |

Estados permitidos: `Proposed`, `Accepted`, `Superseded` y `Rejected`. Una decisión reemplazada enlaza el ADR que la sustituye; no se reescribe su historia.
