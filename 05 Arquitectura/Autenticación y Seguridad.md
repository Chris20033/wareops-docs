# Autenticación y Seguridad

## Tokens y sesión

- Contraseñas con Argon2id y parámetros documentados en código para permitir su actualización.
- Access token JWT de 15 minutos con `sub`, `sessionId`, `iat`, `exp` e `iss`; no contiene la organización activa ni permisos.
- Refresh token opaco de 256 bits, 7 días, almacenado sólo como hash y rotado en cada renovación.
- Cookie de refresh `HttpOnly`, `Secure` en despliegue, `SameSite=Lax` si web y API comparten sitio y ruta limitada a `/api/v1/auth`.
- Reutilizar un refresh ya rotado revoca la sesión asociada. Logout revoca la sesión y elimina la cookie.

## Contexto multiempresa

`X-Organization-Id` es obligatorio en endpoints de negocio. Un guard carga una membresía activa para `sub + organizationId`. Repositorios reciben `organizationId` como argumento obligatorio y lo incluyen en búsquedas, relaciones, conteos y mutaciones.

Un ID existente en otro tenant se responde como `404` cuando revelar su existencia constituya fuga. Relaciones cruzadas se rechazan antes de escribir.

## Autorización

Decoradores declaran permisos estables como `inventory:write`; un guard los compara con el rol de la membresía. Las reglas contextuales —por ejemplo, último propietario— permanecen en el servicio de dominio.

## Riesgos web

- CORS permite exclusivamente `WEB_ORIGIN`, credenciales y headers definidos.
- La cookie sólo se usa para refresh; ese endpoint exige origen permitido. Si el despliegue requiere `SameSite=None`, se añadirá token CSRF de doble envío antes de habilitarlo.
- Zod mejora UX, pero toda entrada vuelve a validarse en NestJS.
- Headers de seguridad se configuran en web/API y no se renderiza HTML aportado por usuarios.
- Rate limiting queda post-MVP; login registra fallos sin incluir credenciales.

## Auditoría y secretos

El serializador de auditoría trabaja con listas permitidas de campos. Passwords, hashes, tokens, cookies, cabeceras de autorización y variables de entorno se redactan también en logs. Archivos `.env.example` contienen sólo nombres y valores ficticios.
