# Decisiones y Supuestos

## Decisiones iniciales

1. El MVP administra órdenes de salida; las órdenes de compra quedan para después del MVP.
2. Los proveedores forman parte del catálogo y pueden asociarse a productos y entradas, sin implementar todavía un ciclo completo de compras.
3. Los roles son predefinidos en el MVP. Los permisos se modelan y se validan, pero no habrá un editor de roles personalizados.
4. Una sucursal puede contener uno o varios almacenes.
5. No se permiten existencias físicas ni disponibles negativas.
6. Las transferencias entre almacenes de una misma organización son atómicas.
7. Todos los identificadores públicos serán UUID.
8. Las cantidades de inventario se almacenan como enteros. Productos fraccionables quedan fuera del MVP.
9. Redis no es requisito del MVP. Se incorporará sólo cuando exista un caso demostrado para caché, limitación de solicitudes o tareas.
10. El despliegue de demostración puede usar servicios administrados; Docker Compose será el entorno local reproducible.

11. Una cuenta puede pertenecer a varias organizaciones mediante membresías independientes.
12. El umbral de mínimo pertenece a la combinación producto-almacén.
13. Cada orden de salida se abastece desde un único almacén.
14. Las invitaciones usan un enlace copiable con token de 72 horas; el MVP no envía correo.
15. El access token se conserva en memoria y el refresh token se rota mediante una cookie segura.
16. La organización activa se envía en `X-Organization-Id` y siempre se valida contra una membresía activa.
17. Los proveedores se relacionan con productos y entradas, sin precios ni ciclo de compras.
18. Las eliminaciones de catálogos con historial son lógicas mediante un estado activo/inactivo.
19. El modelo persistente cumple 3FN y Prisma Client es la única capa de acceso a PostgreSQL.
20. No se usarán consultas raw, vistas, triggers ni migraciones editadas manualmente en el MVP.

## Supuestos operativos

- La moneda, los costos y la valoración contable quedan fuera del MVP.
- Las fechas se persistirán en UTC y se presentarán según la zona horaria configurable de la organización.
- El despliegue podrá usar servicios administrados sin acoplar la arquitectura a un proveedor.
- Las consultas de lectura se simplifican mediante selectores, relaciones y agregaciones Prisma.

## Criterio para cambiar el alcance

Una decisión pasa al MVP sólo si desbloquea un flujo principal, demuestra una competencia técnica relevante o corrige una inconsistencia del dominio. Todo cambio debe reflejarse en [[01 Producto/Alcance y MVP]], [[06 Roadmap/MVP]] y, cuando corresponda, en un ADR.
