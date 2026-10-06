# Sprint 01 — Identidad y Multi-tenancy

**Estado:** Pending  
**Objetivo:** autenticar personas y aislar cada operación mediante membresías y permisos.

## Dependencias

Sprint 00 completado.

## Backend

- [ ] Añadir modelos Prisma `User`, `Organization` y `Membership`.
- [ ] Añadir modelos Prisma `Role`, `Permission` y `RolePermission`.
- [ ] Añadir modelos Prisma `Invitation` y `RefreshSession`.
- [ ] Crear seed de roles predefinidos.
- [ ] Crear seed de permisos predefinidos.
- [ ] Crear seed de relaciones rol-permiso.
- [ ] Implementar hash Argon2id de contraseñas.
- [ ] Implementar registro de usuario.
- [ ] Implementar creación transaccional de organización inicial.
- [ ] Implementar creación transaccional de membresía `OWNER` inicial.
- [ ] Implementar emisión de access token.
- [ ] Implementar creación de refresh session hasheada.
- [ ] Implementar endpoint de login.
- [ ] Implementar rotación de refresh token.
- [ ] Implementar endpoint de refresh de sesión.
- [ ] Implementar revocación de refresh session.
- [ ] Implementar endpoint de logout.
- [ ] Implementar endpoint de perfil autenticado.
- [ ] Implementar listado de organizaciones accesibles.
- [ ] Implementar lectura de organización activa.
- [ ] Implementar actualización de organización para `OWNER`.
- [ ] Implementar guard JWT.
- [ ] Implementar guard de `X-Organization-Id`.
- [ ] Implementar guard de permisos por rol.
- [ ] Implementar listado de membresías.
- [ ] Implementar cambio de rol de una membresía.
- [ ] Implementar activación y desactivación de membresía.
- [ ] Impedir desactivar al último `OWNER` activo.
- [ ] Implementar creación de invitación con enlace copiable.
- [ ] Implementar listado de invitaciones.
- [ ] Implementar revocación de invitación pendiente.
- [ ] Implementar aceptación de invitación para usuario existente.
- [ ] Implementar aceptación de invitación con creación de cuenta.
- [ ] Validar que el correo de aceptación coincida con el correo invitado.

## Frontend

- [ ] Crear cliente HTTP que adjunte access token.
- [ ] Crear cliente HTTP que adjunte `X-Organization-Id`.
- [ ] Crear pantalla de registro.
- [ ] Crear formulario de registro con Zod.
- [ ] Crear pantalla de inicio de sesión.
- [ ] Crear formulario de inicio de sesión con Zod.
- [ ] Restaurar la sesión mediante refresh al cargar la aplicación.
- [ ] Crear store de sesión en Zustand.
- [ ] Crear store de organización activa en Zustand.
- [ ] Crear selector de organización activa.
- [ ] Crear layout de rutas protegidas.
- [ ] Redirigir a login cuando falle la renovación de sesión.
- [ ] Crear pantalla de perfil.
- [ ] Crear listado de miembros.
- [ ] Crear formulario de cambio de rol.
- [ ] Crear acción de activar o desactivar un miembro.
- [ ] Crear formulario de invitación.
- [ ] Mostrar y copiar el enlace de invitación generado.
- [ ] Crear pantalla de aceptación de invitación.
- [ ] Ocultar acciones no autorizadas según permisos recibidos.

## Documentación

- [ ] Documentar DTO y respuestas de registro en OpenAPI.
- [ ] Documentar DTO y respuestas de login en OpenAPI.
- [ ] Documentar refresh y logout en OpenAPI.
- [ ] Documentar cabecera `X-Organization-Id` en OpenAPI.
- [ ] Documentar endpoints de miembros e invitaciones en OpenAPI.
- [ ] Actualizar el diagrama de autenticación.
- [ ] Sincronizar la matriz de permisos con los datos semilla.

## Pruebas

- [ ] Probar que una contraseña se persiste como hash Argon2id.
- [ ] Probar que un refresh token no se persiste en texto plano.
- [ ] Probar rotación y revocación de refresh session.
- [ ] Probar que un recurso de otra organización responde sin revelar datos.
- [ ] Probar que filtros y conteos quedan aislados al tenant activo.
- [ ] Probar que una relación entre tenants se rechaza.
- [ ] Probar que `VIEWER` no puede mutar recursos.
- [ ] Probar que `OPERATOR` no administra miembros.
- [ ] Probar que `OPERATOR` no consulta auditoría.
- [ ] Probar que una invitación sólo se acepta una vez.
- [ ] Probar que una invitación expirada se rechaza.
- [ ] Probar que una invitación revocada se rechaza.
- [ ] Probar que otro correo no acepta una invitación.
- [ ] Probar que siempre permanece un `OWNER` activo.

**Trazabilidad:** RF-001–006; RNF-001–005; CA-001–003, CA-016–019.

## Cierre del sprint

- [ ] Dos organizaciones semilla permiten demostrar aislamiento, cambio de tenant, permisos y renovación segura de sesión.

