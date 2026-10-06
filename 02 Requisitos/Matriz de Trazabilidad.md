# Matriz de Trazabilidad

Esta matriz conecta requisitos y criterios con el sprint que entrega la conducta y con su evidencia principal. Las pruebas de API usan Jest/Supertest y PostgreSQL real cuando intervienen restricciones o concurrencia; la web usa Vitest/RTL y Playwright.

## Requisitos funcionales

| Identificadores | Sprint | Evidencia principal |
| --- | --- | --- |
| RF-001, RF-002, RF-003 | [[../06 Roadmap/Sprints/Sprint 02 - Identidad y Multi-tenancy|Sprint 02]] | Integración de registro/sesión y E2E de acceso/cambio de organización. |
| RF-004, RF-005, RF-006 | [[../06 Roadmap/Sprints/Sprint 02 - Identidad y Multi-tenancy|Sprint 02]] | Matriz de autorización y pruebas negativas entre tenants. |
| RF-007, RF-008, RF-009 | [[../06 Roadmap/Sprints/Sprint 03 - Ubicaciones y Catálogo|Sprint 03]] | Integración CRUD y componentes de formularios/listados. |
| RF-010, RF-011, RF-012 | [[../06 Roadmap/Sprints/Sprint 03 - Ubicaciones y Catálogo|Sprint 03]] | Restricciones únicas, filtros, paginación y estado de URL. |
| RF-013, RF-014, RF-015 | [[../06 Roadmap/Sprints/Sprint 04 - Núcleo de Inventario|Sprint 04]] | Integración de saldos, entradas y salidas. |
| RF-016, RF-017, RF-020 | [[../06 Roadmap/Sprints/Sprint 04 - Núcleo de Inventario|Sprint 04]] | Ajustes, invariantes y ledger inmutable. |
| RF-021, RF-022 | [[../06 Roadmap/Sprints/Sprint 04 - Núcleo de Inventario|Sprint 04]] | Pruebas idempotentes y concurrentes con PostgreSQL. |
| RF-018, RF-019 | [[../06 Roadmap/Sprints/Sprint 05 - Transferencias|Sprint 05]] | Integración de commit y rollback de transferencia. |
| RF-023, RF-024, RF-025, RF-026 | [[../06 Roadmap/Sprints/Sprint 06 - Órdenes y Reservas|Sprint 06]] | Ciclo de borrador y confirmación todo-o-nada. |
| RF-027, RF-028, RF-029 | [[../06 Roadmap/Sprints/Sprint 06 - Órdenes y Reservas|Sprint 06]] | Finalización, cancelación y estados terminales. |
| RF-030, RF-031 | [[../06 Roadmap/Sprints/Sprint 07 - Supervisión|Sprint 07]] | Consultas de dashboard y alertas verificadas con fixtures. |
| RF-032, RF-033 | [[../06 Roadmap/Sprints/Sprint 07 - Supervisión|Sprint 07]] | Auditoría transaccional, redacción, filtros y permisos. |
| RF-034 | [[../06 Roadmap/Sprints/Sprint 01 - Fundación|Sprint 01]] | OpenAPI y pruebas de liveness/readiness. |

## Requisitos no funcionales

| Identificadores | Sprint | Evidencia principal |
| --- | --- | --- |
| RNF-001, RNF-002, RNF-004 | [[../06 Roadmap/Sprints/Sprint 02 - Identidad y Multi-tenancy|Sprint 02]] | Hashes, rotación, redacción y pruebas de sesión. |
| RNF-003, RNF-005 | [[../06 Roadmap/Sprints/Sprint 02 - Identidad y Multi-tenancy|Sprint 02]] | Guards de tenant y validación de límites. |
| RNF-006, RNF-007, RNF-008, RNF-009 | [[../06 Roadmap/Sprints/Sprint 04 - Núcleo de Inventario|Sprint 04]] | Transacciones, carreras e idempotencia. |
| RNF-010, RNF-011, RNF-012 | [[../06 Roadmap/Sprints/Sprint 08 - Cierre de Portafolio|Sprint 08]] | Dataset de volumen y reporte de percentiles. |
| RNF-013, RNF-014 | [[../06 Roadmap/Sprints/Sprint 01 - Fundación|Sprint 01]] | TypeScript estricto y CI. |
| RNF-015 | [[../06 Roadmap/Sprints/Sprint 04 - Núcleo de Inventario|Sprint 04]] | Cobertura de reglas críticas e integración. |
| RNF-016 | [[../06 Roadmap/Sprints/Sprint 01 - Fundación|Sprint 01]] | Proceso e índice ADR. |
| RNF-017 | [[../06 Roadmap/Sprints/Sprint 01 - Fundación|Sprint 01]] | Verificación OpenAPI en CI. |
| RNF-018, RNF-019, RNF-020 | [[../06 Roadmap/Sprints/Sprint 08 - Cierre de Portafolio|Sprint 08]] | Playwright, auditoría de teclado/contraste y UX de errores. |
| RNF-021, RNF-022, RNF-023 | [[../06 Roadmap/Sprints/Sprint 01 - Fundación|Sprint 01]] | Docker Compose, captura de logs y health checks. |
| RNF-024 | [[../06 Roadmap/Sprints/Sprint 08 - Cierre de Portafolio|Sprint 08]] | Pruebas de persistencia UTC y presentación por zona IANA. |

## Criterios de aceptación

| Identificadores | Sprint | Tipo de prueba |
| --- | --- | --- |
| CA-001, CA-002, CA-003 | [[../06 Roadmap/Sprints/Sprint 02 - Identidad y Multi-tenancy|Sprint 02]] | Integración negativa multiempresa. |
| CA-004, CA-005, CA-006 | [[../06 Roadmap/Sprints/Sprint 04 - Núcleo de Inventario|Sprint 04]] | Integración y concurrencia. |
| CA-007, CA-008, CA-009 | [[../06 Roadmap/Sprints/Sprint 05 - Transferencias|Sprint 05]] | Atomicidad, rollback e idempotencia. |
| CA-010, CA-011, CA-012 | [[../06 Roadmap/Sprints/Sprint 06 - Órdenes y Reservas|Sprint 06]] | Almacén único, reserva total y exclusión. |
| CA-013, CA-014, CA-015 | [[../06 Roadmap/Sprints/Sprint 06 - Órdenes y Reservas|Sprint 06]] | Cancelación, finalización y reintento. |
| CA-016, CA-017 | [[../06 Roadmap/Sprints/Sprint 02 - Identidad y Multi-tenancy|Sprint 02]] | Autorización por rol. |
| CA-018, CA-019 | [[../06 Roadmap/Sprints/Sprint 07 - Supervisión|Sprint 07]] | Auditoría y redacción. |
| CA-020, CA-021 | [[../06 Roadmap/Sprints/Sprint 03 - Ubicaciones y Catálogo|Sprint 03]] | URL, formularios y componentes. |
| CA-022 | [[../06 Roadmap/Sprints/Sprint 01 - Fundación|Sprint 01]] | Contrato OpenAPI. |
| CA-023 | [[../06 Roadmap/Sprints/Sprint 08 - Cierre de Portafolio|Sprint 08]] | Playwright sobre entorno desplegado. |
