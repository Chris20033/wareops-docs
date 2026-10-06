# Usuarios y Roles

## Modelo de acceso

Una persona se representa como usuario global y accede a cada organización mediante una membresía. El rol pertenece a la membresía, no al usuario global. Cada solicitud opera dentro de una organización activa.

## Roles predefinidos

| Rol | Capacidades principales |
| --- | --- |
| Propietario (`OWNER`) | Control total, miembros, roles operativos y configuración de organización. |
| Administrador (`ADMIN`) | Gestión operativa y de usuarios, excepto acciones exclusivas del propietario. |
| Gerente (`MANAGER`) | Catálogos, inventario, órdenes, dashboard y auditoría de lectura. |
| Operador (`OPERATOR`) | Consulta y ejecución de entradas, salidas, transferencias y órdenes según permiso. |
| Lector (`VIEWER`) | Acceso de sólo lectura a catálogos, inventario y dashboard. |

## Matriz resumida

| Capacidad | OWNER | ADMIN | MANAGER | OPERATOR | VIEWER |
| --- | :---: | :---: | :---: | :---: | :---: |
| Gestionar organización | Sí | No | No | No | No |
| Gestionar miembros | Sí | Sí | No | No | No |
| Gestionar catálogos | Sí | Sí | Sí | No | No |
| Operar inventario | Sí | Sí | Sí | Sí | No |
| Gestionar órdenes | Sí | Sí | Sí | Sí | No |
| Ver auditoría | Sí | Sí | Sí | No | No |
| Consultar dashboard | Sí | Sí | Sí | Sí | Sí |

## Permisos

La API autoriza mediante permisos estables, por ejemplo `catalog:write`, `inventory:write` y `audit:read`. Roles, permisos y su relación se modelan en tablas normalizadas y se cargan como datos semilla. Aunque el MVP no incluye roles personalizados, este diseño evita dispersar comparaciones de nombres de rol en el código.
