# Plan de Sprints

Los sprints se completan por objetivo y no tienen fechas rígidas. Cada uno entrega API, web, documentación y pruebas cuando aplique.

## Seguimiento con checkboxes

Cada archivo de sprint contiene checkboxes de entregables, pruebas y cierre. Marca una tarea sólo cuando exista evidencia verificable —código, prueba, CI o documentación sincronizada—. Al completar todos los checks de cierre, cambia su `Estado` a `Completed` y actualiza [[MVP]]. Si hay trabajo iniciado, usa `In Progress`; el trabajo descartado debe conservarse como `Deferred` con una nota de motivo.

| Sprint | Resultado demostrable | Trazabilidad principal |
| --- | --- | --- |
| [[Sprints/Sprint 01 - Fundación|01 — Fundación]] | Proyectos ejecutables, CI, PostgreSQL y health checks. | RF-034; RNF-013, 014, 017, 021–023; CA-022 |
| [[Sprints/Sprint 02 - Identidad y Multi-tenancy|02 — Identidad y multi-tenancy]] | Sesión segura, cambio de organización, miembros y RBAC. | RF-001–006; RNF-001–005; CA-001–003, 016–019 |
| [[Sprints/Sprint 03 - Ubicaciones y Catálogo|03 — Ubicaciones y catálogo]] | CRUD navegable de sucursales, almacenes, productos y proveedores. | RF-007–012; CA-020–021 |
| [[Sprints/Sprint 04 - Núcleo de Inventario|04 — Núcleo de inventario]] | Entradas, salidas, ajustes y ledger consistentes. | RF-013–017, 020–022; RNF-006–011, 015; CA-004–006, 009 |
| [[Sprints/Sprint 05 - Transferencias|05 — Transferencias]] | Transferencia atómica e idempotente. | RF-018–019; CA-007–009 |
| [[Sprints/Sprint 06 - Órdenes y Reservas|06 — Órdenes y reservas]] | Ciclo completo de orden con reserva. | RF-023–029; CA-010–015 |
| [[Sprints/Sprint 07 - Supervisión|07 — Supervisión]] | Dashboard, mínimos y auditoría filtrable. | RF-030–033; CA-002, 018–020 |
| [[Sprints/Sprint 08 - Cierre de Portafolio|08 — Cierre de portafolio]] | Demo desplegada, accesible y probada E2E. | RNF-010–012, 016–024; CA-021–023 |

## Regla de avance

Un sprint sólo termina cuando su definición de terminado y pruebas pasan. Una tarea incompleta se mantiene en el mismo sprint o se marca `Deferred` actualizando [[../01 Producto/Alcance y MVP|Alcance y MVP]]; no se oculta moviéndola silenciosamente.
