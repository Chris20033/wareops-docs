# Requisitos Funcionales

## Identidad y organizaciones

- **RF-001:** El sistema permitirá registrar una cuenta y crear su organización inicial.
- **RF-002:** El sistema permitirá iniciar sesión, renovar la sesión y cerrarla.
- **RF-003:** El sistema permitirá a un usuario seleccionar una organización entre sus membresías activas.
- **RF-004:** El sistema impedirá consultar o modificar recursos pertenecientes a otra organización.
- **RF-005:** Un propietario o administrador podrá crear invitaciones con enlace temporal, listar miembros, cambiar su rol y desactivarlos conforme a sus permisos.
- **RF-006:** El sistema autorizará cada operación protegida mediante permisos asociados al rol de la membresía.

## Ubicaciones y catálogos

- **RF-007:** Un usuario autorizado podrá crear, consultar, editar y desactivar sucursales.
- **RF-008:** Un usuario autorizado podrá crear, consultar, editar y desactivar almacenes asociados a una sucursal.
- **RF-009:** Un usuario autorizado podrá crear, consultar, editar y desactivar productos.
- **RF-010:** El sistema garantizará que el SKU de un producto sea único dentro de la organización.
- **RF-011:** Un usuario autorizado podrá crear, consultar, editar y desactivar proveedores.
- **RF-012:** Los listados permitirán búsqueda, filtros y paginación.

## Inventario

- **RF-013:** El sistema mostrará existencia física, reservada y disponible por producto y almacén.
- **RF-014:** Un usuario autorizado podrá registrar entradas con cantidad, motivo y referencia opcional.
- **RF-015:** Un usuario autorizado podrá registrar salidas si existe cantidad disponible suficiente.
- **RF-016:** Un usuario autorizado podrá registrar ajustes positivos o negativos con motivo obligatorio.
- **RF-017:** El sistema rechazará cualquier operación que produzca existencias físicas o disponibles negativas.
- **RF-018:** Un usuario autorizado podrá transferir existencias entre dos almacenes activos de la misma organización.
- **RF-019:** Una transferencia se completará de forma íntegra o no producirá cambios.
- **RF-020:** El sistema conservará un historial inmutable y paginado de movimientos.
- **RF-021:** Los comandos críticos admitirán una clave de idempotencia para evitar efectos duplicados.
- **RF-022:** Las actualizaciones concurrentes sobre las mismas existencias mantendrán las invariantes del inventario.

## Órdenes y reservas

- **RF-023:** Un usuario autorizado podrá crear y editar una orden de salida en borrador, asignada a un almacén activo, con uno o más renglones.
- **RF-024:** Cada renglón indicará un producto único dentro de la orden y una cantidad entera positiva.
- **RF-025:** Confirmar una orden reservará sus unidades de forma atómica.
- **RF-026:** Si algún renglón no tiene disponibilidad suficiente, no se confirmará ningún renglón de la orden.
- **RF-027:** Completar una orden reducirá la existencia física y liberará la reserva correspondiente.
- **RF-028:** Cancelar una orden confirmada liberará sus reservas sin reducir la existencia física.
- **RF-029:** Una orden completada o cancelada no podrá modificarse ni cambiar nuevamente de estado.

## Supervisión

- **RF-030:** El dashboard mostrará productos activos, almacenes activos, órdenes por estado, alertas de mínimo y movimientos recientes.
- **RF-031:** El sistema identificará como bajo mínimo un inventario cuya disponibilidad sea menor o igual al umbral configurado para ese producto y almacén.
- **RF-032:** El sistema registrará en auditoría las acciones sensibles con actor, fecha, organización, acción, entidad y cambios relevantes.
- **RF-033:** Un usuario autorizado podrá filtrar y paginar los eventos de auditoría.
- **RF-034:** La API expondrá su contrato mediante OpenAPI y un endpoint de salud.
