# Alcance y MVP

## Incluido en el MVP

- Autenticación con access token y refresh token.
- Creación inicial de organización y selección de organización activa.
- Usuarios, invitaciones simples, membresías, roles y permisos predefinidos.
- CRUD con activación/desactivación de sucursales, almacenes, productos y proveedores.
- SKU único por organización.
- Consulta de existencias físicas, reservadas y disponibles por producto y almacén.
- Entradas, salidas justificadas y ajustes.
- Transferencias atómicas entre almacenes.
- Órdenes de salida abastecidas desde un único almacén, con borrador, confirmación, reserva, finalización y cancelación.
- Prevención de inventario negativo y control de concurrencia.
- Claves de idempotencia en comandos críticos de inventario.
- Historial de movimientos y registro de auditoría.
- Alertas de existencias mínimas por producto y almacén, calculadas al consultar.
- Invitaciones de miembros mediante enlace copiable con expiración, sin envío de correo.
- Dashboard, búsqueda, filtros y paginación.
- Swagger/OpenAPI, health check, logs estructurados y Docker Compose local.
- Pruebas unitarias, integración de reglas críticas y un recorrido E2E principal.

## Fuera del MVP

- Órdenes de compra y recepción parcial de compras.
- Lotes, números de serie, fechas de caducidad y unidades fraccionables.
- Valoración contable, facturación, impuestos y pagos.
- Importación o exportación masiva.
- Notificaciones por correo, SMS o push.
- Roles personalizados desde la interfaz.
- Redis, colas y procesos en segundo plano.
- Aplicaciones móviles, modo sin conexión e internacionalización completa.
- Integraciones con ERP, comercio electrónico o transportistas.
- Analítica avanzada y pronósticos de demanda.

## Recorrido demostrable

1. El usuario inicia sesión en una organización de demostración.
2. Consulta el dashboard y detecta un producto bajo mínimo.
3. Registra una entrada en un almacén.
4. Transfiere parte de las unidades a otra ubicación.
5. Crea y confirma una orden de salida, reservando inventario.
6. Completa la orden y observa el movimiento y la auditoría resultantes.

## Definición de terminado del producto

El MVP se considera terminado cuando todos los elementos marcados como obligatorios en [[06 Roadmap/MVP]] están completados, los criterios de aceptación críticos pasan en CI y el recorrido demostrable puede ejecutarse en un entorno desplegado.
