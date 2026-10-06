# Sprint 07 — Cierre de Portafolio

**Estado:** Pending  
**Objetivo:** publicar una demostración reproducible, accesible y respaldada por evidencia técnica.

## Dependencias

Sprints 00–06 completados.

## Backend

- [ ] Revisar que todos los endpoints protegidos validen tenant y permiso.
- [ ] Revisar que los DTO no expongan hashes, tokens ni secretos.
- [ ] Revisar que todos los comandos críticos requieran `Idempotency-Key`.
- [ ] Revisar que todos los comandos críticos creen auditoría.
- [ ] Verificar que Swagger coincida con controladores y DTO implementados.
- [ ] Verificar que no exista `$queryRaw`, `$executeRaw` ni TypedSQL.

## Frontend

- [ ] Revisar estados de carga de consultas principales.
- [ ] Revisar estados de error de consultas principales.
- [ ] Revisar estados vacíos de listados principales.
- [ ] Verificar navegación por teclado en formularios críticos.
- [ ] Verificar foco visible en controles críticos.
- [ ] Verificar etiquetas accesibles en formularios críticos.
- [ ] Verificar contraste equivalente a WCAG 2.1 AA.
- [ ] Verificar experiencia responsive en escritorio.
- [ ] Verificar experiencia responsive en tablet.
- [ ] Verificar operaciones críticas en móvil.

## Datos e Infraestructura

- [ ] Crear seed de organización de demostración.
- [ ] Crear seed de usuarios con cada rol.
- [ ] Crear seed de inventario bajo mínimo.
- [ ] Crear seed del recorrido completo de operaciones.
- [ ] Generar dataset de 100 000 movimientos para medición.
- [ ] Medir p95 de lecturas paginadas comunes.
- [ ] Medir tiempo de carga de dashboard.
- [ ] Configurar build de imagen Docker de la API.
- [ ] Configurar health check de imagen API.
- [ ] Configurar despliegue de PostgreSQL administrado.
- [ ] Configurar despliegue de API con HTTPS.
- [ ] Configurar despliegue de web con HTTPS.
- [ ] Configurar variables de entorno separadas para demo.
- [ ] Configurar CORS del entorno desplegado.
- [ ] Configurar cookies seguras del entorno desplegado.
- [ ] Ejecutar migraciones Prisma como paso único de despliegue.
- [ ] Verificar `/health/live` en el entorno desplegado.
- [ ] Verificar `/health/ready` en el entorno desplegado.
- [ ] Crear workflow E2E de GitHub Actions.

## Documentación

- [ ] Actualizar README de API con URL y comandos de demo.
- [ ] Actualizar README de web con URL de demo.
- [ ] Documentar variables de entorno requeridas para despliegue.
- [ ] Documentar procedimiento de migración de despliegue.
- [ ] Documentar credenciales de demo fuera del código productivo.
- [ ] Crear guion del recorrido de portafolio.
- [ ] Revisar que arquitectura, ADR y OpenAPI coincidan con la implementación.
- [ ] Actualizar estado del MVP con evidencia de cierre.

## Pruebas

- [ ] Crear prueba Playwright de inicio de sesión.
- [ ] Crear prueba Playwright de alerta de mínimo.
- [ ] Crear prueba Playwright de entrada de inventario.
- [ ] Crear prueba Playwright de transferencia.
- [ ] Crear prueba Playwright de confirmación de orden.
- [ ] Crear prueba Playwright de finalización de orden.
- [ ] Crear prueba Playwright de movimientos resultantes.
- [ ] Crear prueba Playwright de auditoría resultante.
- [ ] Ejecutar el recorrido E2E en entorno de pruebas.
- [ ] Ejecutar el recorrido E2E desplegado.
- [ ] Verificar p95 menor a 500 ms en lecturas definidas.
- [ ] Verificar dashboard menor a 2 segundos en entorno de demostración.
- [ ] Ejecutar auditoría manual de accesibilidad.
- [ ] Ejecutar revisión de secretos en repositorios y logs.
- [ ] Ejecutar instalación limpia desde README.
- [ ] Verificar que CI de API pase.
- [ ] Verificar que CI de web pase.

**Trazabilidad:** RNF-010–024; CA-021–023 y recorrido demostrable del producto.

## Cierre del sprint

- [ ] El MVP está desplegado, su recorrido se reproduce sin intervención técnica y toda afirmación central del portafolio tiene prueba o documentación enlazada.
