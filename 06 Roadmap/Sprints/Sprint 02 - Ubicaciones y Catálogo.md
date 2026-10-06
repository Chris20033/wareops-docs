# Sprint 02 — Ubicaciones y Catálogo

**Estado:** Pending  
**Objetivo:** administrar las entidades necesarias para operar inventario.

## Dependencias

Sprint 01 completado.

## Backend

- [ ] Añadir modelos Prisma `Branch` y `Warehouse`.
- [ ] Añadir modelos Prisma `Product`, `Supplier` y `ProductSupplier`.
- [ ] Implementar creación de sucursal.
- [ ] Implementar listado paginado de sucursales.
- [ ] Implementar detalle de sucursal.
- [ ] Implementar actualización de sucursal.
- [ ] Implementar desactivación de sucursal.
- [ ] Implementar creación de almacén.
- [ ] Implementar listado paginado de almacenes.
- [ ] Implementar detalle de almacén.
- [ ] Implementar actualización de almacén.
- [ ] Implementar desactivación de almacén.
- [ ] Implementar creación de producto.
- [ ] Implementar listado paginado de productos.
- [ ] Implementar detalle de producto.
- [ ] Implementar actualización de producto.
- [ ] Implementar desactivación de producto.
- [ ] Implementar creación de proveedor.
- [ ] Implementar listado paginado de proveedores.
- [ ] Implementar detalle de proveedor.
- [ ] Implementar actualización de proveedor.
- [ ] Implementar desactivación de proveedor.
- [ ] Implementar asociación de proveedor a producto.
- [ ] Implementar listado de proveedores por producto.
- [ ] Implementar eliminación de asociación producto-proveedor.
- [ ] Implementar búsqueda de catálogos.
- [ ] Implementar filtros de catálogos.
- [ ] Implementar ordenamiento de catálogos.
- [ ] Limitar `pageSize` a 100 registros.
- [ ] Normalizar SKU a mayúsculas antes de persistir.
- [ ] Normalizar códigos de sucursal, almacén y proveedor a mayúsculas antes de persistir.

## Frontend

- [ ] Crear listado de sucursales.
- [ ] Crear formulario de sucursal.
- [ ] Crear pantalla de detalle de sucursal.
- [ ] Crear acción de desactivación de sucursal.
- [ ] Crear listado de almacenes.
- [ ] Crear formulario de almacén.
- [ ] Crear pantalla de detalle de almacén.
- [ ] Crear acción de desactivación de almacén.
- [ ] Crear listado de productos.
- [ ] Crear formulario de producto.
- [ ] Crear pantalla de detalle de producto.
- [ ] Crear acción de desactivación de producto.
- [ ] Crear listado de proveedores.
- [ ] Crear formulario de proveedor.
- [ ] Crear pantalla de detalle de proveedor.
- [ ] Crear acción de desactivación de proveedor.
- [ ] Crear selector de proveedores en el detalle de producto.
- [ ] Sincronizar búsqueda, filtros, orden y página con la URL.
- [ ] Mostrar errores de validación junto al campo correspondiente.

## Datos e Infraestructura

- [ ] Crear migración Prisma de ubicaciones.
- [ ] Crear migración Prisma de catálogo.
- [ ] Añadir índices Prisma de listados y búsqueda definidos en el diccionario.
- [ ] Añadir datos seed de sucursales, almacenes, productos y proveedores.

## Documentación

- [ ] Documentar endpoints de sucursales en OpenAPI.
- [ ] Documentar endpoints de almacenes en OpenAPI.
- [ ] Documentar endpoints de productos en OpenAPI.
- [ ] Documentar endpoints de proveedores en OpenAPI.
- [ ] Documentar relación producto-proveedor en OpenAPI.
- [ ] Sincronizar el diccionario de datos con la migración Prisma.

## Pruebas

- [ ] Probar SKU único dentro de la organización.
- [ ] Probar código de sucursal único dentro de la organización.
- [ ] Probar código de almacén único dentro de una sucursal.
- [ ] Probar código de proveedor único dentro de la organización.
- [ ] Probar que un almacén pertenece a una sucursal del tenant activo.
- [ ] Probar que producto y proveedor deben pertenecer al mismo tenant.
- [ ] Probar que un catálogo con historial se desactiva sin eliminarse.
- [ ] Probar búsqueda de cada catálogo.
- [ ] Probar filtros y paginación de cada listado.
- [ ] Probar persistencia de filtros en la URL.
- [ ] Probar validaciones de formularios de catálogo.

**Trazabilidad:** RF-007–012; CA-003, CA-020–021.

## Cierre del sprint

- [ ] Un gerente puede preparar dos sucursales, sus almacenes, productos y proveedores desde la interfaz.
