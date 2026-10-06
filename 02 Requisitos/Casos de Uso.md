# Casos de Uso

## CU-01 — Iniciar sesión

**Actor:** miembro activo.  
**Flujo principal:** introduce credenciales, el servidor valida la cuenta y devuelve una sesión asociada a una organización permitida.  
**Alternativas:** credenciales inválidas, membresía inactiva o sesión expirada.

## CU-02 — Administrar catálogo

**Actor:** gerente o superior.  
**Flujo principal:** crea o actualiza un producto con SKU único y umbral de mínimo opcional.  
**Alternativas:** SKU duplicado, datos inválidos o falta de permiso.

## CU-03 — Registrar entrada

**Actor:** operador autorizado.  
**Precondiciones:** producto y almacén activos, cantidad positiva.  
**Flujo principal:** envía la operación con clave de idempotencia; el sistema incrementa existencia, crea movimiento y auditoría en una transacción.  
**Alternativas:** recurso ajeno a la organización o reutilización inválida de clave.

## CU-04 — Registrar salida o ajuste negativo

**Actor:** operador autorizado.  
**Precondiciones:** disponibilidad suficiente.  
**Flujo principal:** el sistema descuenta atómicamente, registra movimiento y auditoría.  
**Alternativa:** si otra operación consume las unidades primero, la solicitud se rechaza sin cambios parciales.

## CU-05 — Transferir inventario

**Actor:** operador autorizado.  
**Precondiciones:** almacenes distintos, activos y de la misma organización.  
**Flujo principal:** una transacción Prisma serializable valida y actualiza condicionalmente origen y destino, y genera dos movimientos unidos por una transferencia.  
**Alternativas:** disponibilidad insuficiente, almacén inválido o solicitud duplicada.

## CU-06 — Procesar orden de salida

**Actor:** operador autorizado.  
**Flujo principal:** crea un borrador para un almacén, agrega productos, confirma para reservar y completa para descontar existencia.  
**Alternativas:** confirmación sin disponibilidad; cancelación libera reservas; una orden terminal no admite cambios.

## CU-07 — Consultar trazabilidad

**Actor:** gerente o superior.  
**Flujo principal:** filtra movimientos o auditoría por fechas, usuario, almacén, producto, acción o entidad y abre el detalle relacionado.

## CU-08 — Supervisar operación

**Actor:** miembro con lectura.  
**Flujo principal:** consulta indicadores, alertas de mínimo y actividad reciente del dashboard dentro de su organización.
