# ADR-002 — Contexto multiempresa

**Estado:** Accepted  
**Fecha:** 2026-09-14

## Contexto

Una cuenta puede pertenecer a varias organizaciones. Incluir un tenant fijo en el JWT obliga a emitir tokens al cambiar y puede dejar permisos obsoletos hasta su expiración.

## Decisión

El JWT identifica usuario y sesión. La web envía la organización activa en `X-Organization-Id`; la API valida en cada solicitud una membresía activa y obtiene de ella el rol. Repositorios y relaciones reciben el tenant explícitamente.

## Consecuencias

- Cambiar organización no requiere emitir un access token.
- Desactivar membresía o cambiar rol tiene efecto inmediato.
- Cada consulta debe filtrar tenant; pruebas de aislamiento y claves compuestas reducen omisiones.
- No se adopta Row-Level Security en el MVP; puede añadirse como defensa adicional futura.
