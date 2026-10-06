# Visión del Producto

## Problema

Las empresas con varias ubicaciones suelen fragmentar su inventario en hojas de cálculo o sistemas aislados. Esto dificulta conocer qué producto existe, dónde está, qué parte ya está comprometida y quién modificó la información.

## Propuesta de valor

WareOps centraliza sucursales, almacenes, productos, proveedores, órdenes y movimientos. Ofrece una vista actual del inventario y un historial verificable de operaciones, manteniendo separados los datos de cada organización.

## Usuarios objetivo

- Pequeñas y medianas empresas con varias ubicaciones.
- Responsables de inventario y operaciones.
- Personal de almacén que registra entradas, salidas y transferencias.
- Supervisores que necesitan indicadores y trazabilidad.

## Objetivos del producto

- Reducir errores al conocer existencias físicas, reservadas y disponibles.
- Evitar operaciones que produzcan inventario negativo.
- Permitir rastrear cada cambio de inventario.
- Separar estrictamente la información entre organizaciones.
- Facilitar la demostración del sistema mediante datos semilla y flujos completos.

## Objetivo de portafolio

Demostrar una aplicación full stack cercana a producción en sus decisiones esenciales: diseño modular, multi-tenancy, RBAC, transacciones, concurrencia, idempotencia, auditoría, pruebas, CI y despliegue reproducible. No busca cubrir la amplitud de un ERP.

## Indicadores de éxito del MVP

- Un usuario puede completar el recorrido desde inicio de sesión hasta una operación de inventario.
- Una transferencia nunca deja un resultado parcial.
- Dos operaciones concurrentes no pueden consumir las mismas unidades.
- Un usuario de una organización no puede consultar ni modificar datos de otra.
- Los movimientos y eventos de auditoría permiten reconstruir acciones relevantes.
- El repositorio puede instalarse, probarse y ejecutarse siguiendo su documentación.
