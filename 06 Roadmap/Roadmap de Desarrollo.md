# Roadmap de Desarrollo

## Fase 1 — Base segura

Los sprints 1 y 2 crean repositorios ejecutables, automatización, autenticación, tenant y permisos. Al finalizar, un usuario puede entrar, cambiar de organización y administrar miembros sin fugas de datos.

## Fase 2 — Operación de inventario

Los sprints 3 a 6 entregan catálogos, saldos, movimientos, transferencias y órdenes mediante cortes verticales de API y web. Cada incremento debe ser demostrable antes de avanzar.

## Fase 3 — Supervisión y publicación

Los sprints 7 y 8 añaden dashboard, auditoría, accesibilidad, volumen de prueba, E2E y despliegue. El resultado debe contar una historia técnica verificable, no sólo mostrar pantallas.

## Secuencia

```mermaid
flowchart LR
    S1[1 Fundación] --> S2[2 Identidad]
    S2 --> S3[3 Catálogo]
    S3 --> S4[4 Inventario]
    S4 --> S5[5 Transferencias]
    S5 --> S6[6 Órdenes]
    S6 --> S7[7 Supervisión]
    S7 --> S8[8 Cierre]
```

El detalle y la trazabilidad están en [[Plan de Sprints]].
