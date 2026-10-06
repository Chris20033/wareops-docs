# Sprint 00 — Fundación

**Estado:** Pending  
**Objetivo:** disponer de API, web y base de datos ejecutables con calidad automatizada.

## Dependencias

Documentación funcional aprobada y versiones LTS compatibles de Node.js.

## Backend

- [ ] Crear el proyecto NestJS en `wareops-api`.
- [ ] Activar TypeScript estricto en la API.
- [ ] Configurar ESLint y Prettier en la API.
- [ ] Instalar y configurar Prisma con PostgreSQL.
- [ ] Crear el esquema Prisma inicial sin entidades de negocio.
- [ ] Configurar validación de variables de entorno al arrancar.
- [ ] Crear el endpoint `GET /health/live`.
- [ ] Crear el endpoint `GET /health/ready`.
- [ ] Configurar Swagger/OpenAPI bajo `/docs`.
- [ ] Definir el formato global de errores HTTP.
- [ ] Añadir generación y propagación de `requestId`.
- [ ] Configurar logs estructurados JSON.

## Frontend

- [ ] Crear el proyecto Next.js con App Router en `wareops-web`.
- [ ] Activar TypeScript estricto en la web.
- [ ] Configurar ESLint y Prettier en la web.
- [ ] Configurar Tailwind CSS.
- [ ] Inicializar shadcn/ui.
- [ ] Crear el layout raíz de la aplicación.
- [ ] Crear una pantalla mínima, responsiva y accesible que confirme el arranque de WareOps sin anticipar funcionalidades de negocio.
- [ ] Configurar TanStack Query y su `QueryClientProvider`.
- [ ] Crear la estructura inicial de `features`, `components`, `lib`, `stores` y `test`.
- [ ] Configurar Zustand para estado cliente.
- [ ] Configurar Vitest y React Testing Library.

## Datos e Infraestructura

- [ ] Crear `docker-compose.yml` con PostgreSQL local.
- [ ] Crear `.env.example` de la API sin secretos reales.
- [ ] Crear `.env.example` de la web sin secretos reales.
- [ ] Añadir el comando de migración Prisma para desarrollo.
- [ ] Añadir el comando de seed Prisma para desarrollo.
- [ ] Crear el workflow de GitHub Actions para lint de la API.
- [ ] Crear el workflow de GitHub Actions para pruebas de la API.
- [ ] Crear el workflow de GitHub Actions para build de la API.
- [ ] Crear el workflow de GitHub Actions para lint de la web.
- [ ] Crear el workflow de GitHub Actions para pruebas de la web.
- [ ] Crear el workflow de GitHub Actions para build de la web.

## Documentación

- [ ] Crear README de la API con requisitos y comandos locales.
- [ ] Crear README de la web con requisitos y comandos locales.
- [ ] Documentar el arranque de PostgreSQL con Docker Compose.
- [ ] Documentar el flujo de migración y seed de Prisma.
- [ ] Sincronizar las versiones y comandos documentados con ambos repositorios.

## Pruebas

- [ ] Verificar instalación limpia de la API desde su README.
- [ ] Verificar instalación limpia de la web desde su README.
- [ ] Verificar que `health/live` responde sin PostgreSQL.
- [ ] Verificar que `health/ready` falla sin PostgreSQL.
- [ ] Verificar que Swagger carga el formato de error documentado.
- [ ] Verificar que lint, pruebas y build pasan en CI para la API.
- [ ] Verificar que lint, pruebas y build pasan en CI para la web.

**Trazabilidad:** RF-034; RNF-013, RNF-014, RNF-017, RNF-021–023; CA-022.

## Cierre del sprint

- [ ] API, web y PostgreSQL se levantan reproduciblemente; lint, pruebas mínimas y build pasan en local y CI.
