# Módulos Principales

| Módulo | Responsabilidad |
| --- | --- |
| Identidad y acceso | Registro, inicio de sesión, renovación, cierre de sesión y organización activa. |
| Organizaciones | Datos de la empresa, membresías y aislamiento multiempresa. |
| Ubicaciones | Sucursales y almacenes. |
| Catálogo | Productos, SKU, proveedores y relaciones producto-proveedor. |
| Inventario | Existencias, entradas, salidas, ajustes y consulta por ubicación. |
| Transferencias | Traslado atómico entre almacenes. |
| Órdenes | Borradores, reservas, finalización y cancelación de órdenes de salida. |
| Auditoría | Consulta de acciones y cambios relevantes. |
| Dashboard | Indicadores, actividad reciente y alertas de mínimo. |

## Dependencias funcionales

Las ubicaciones y el catálogo alimentan al inventario. El inventario sustenta transferencias y órdenes. Auditoría observa las operaciones de todos los módulos, mientras identidad y organizaciones delimitan cada acción.
