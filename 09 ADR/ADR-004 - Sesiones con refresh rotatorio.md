# ADR-004 — Sesiones con refresh rotatorio

**Estado:** Accepted  
**Fecha:** 2026-09-14

## Contexto

Guardar tokens duraderos en almacenamiento accesible a JavaScript amplifica el impacto de XSS. Usar sólo cookies para toda autenticación aumenta la superficie CSRF.

## Decisión

El access JWT dura 15 minutos y vive en memoria. El refresh es opaco, dura 7 días, viaja en cookie `HttpOnly`/`Secure`, se guarda como hash y rota en cada uso. La sesión durable permite revocación y detección de reutilización.

## Consecuencias

- Una recarga requiere un refresh silencioso.
- XSS no puede leer directamente el token durable.
- CORS, origen y atributos de cookie deben configurarse como unidad.
- Si se necesita `SameSite=None`, será obligatorio añadir protección CSRF antes del despliegue.
