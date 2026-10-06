# Backend

## Base tecnológica

- Node.js 24 LTS y npm 11.
- NestJS 11 con módulos ESM y TypeScript en modo estricto.
- Prisma ORM 7 con el generador `prisma-client` y el adaptador `@prisma/adapter-pg`.
- PostgreSQL 18 como base local y de integración.

## Estructura esperada

```text
src/
├── modules/
│   ├── auth/
│   ├── organizations/
│   ├── catalog/
│   ├── inventory/
│   ├── orders/
│   ├── audit/
│   └── dashboard/
├── common/
│   ├── auth/
│   ├── errors/
│   ├── http/
│   └── observability/
├── database/
├── config/
└── main.ts
```

Cada módulo contiene sólo las piezas que necesita: controller, DTO, service, repository, selector y mapper. Prisma permanece detrás de repositorios o servicios transaccionales; no se devuelve un modelo Prisma directamente.

## Pipeline HTTP

- `ValidationPipe` global con transformación, whitelist y rechazo de propiedades desconocidas.
- Guard JWT seguido de resolución de organización y guard de permisos.
- Interceptor para `requestId`, respuesta consistente y logging.
- Filtro global que traduce errores de dominio a códigos HTTP estables.
- Documentación Swagger con esquemas de éxito y error.
- Las rutas de negocio usan `/api/v1`; `/health/live`, `/health/ready`, `/docs` y `/docs-json` permanecen fuera del prefijo.
- `X-Request-Id` acepta un UUID proporcionado por el cliente o genera uno nuevo. Un valor presente pero inválido responde `400 VALIDATION_ERROR` con un nuevo identificador seguro.

## Persistencia y concurrencia

- Prisma Client es la única API de acceso a datos: no se permiten operaciones raw.
- Prisma Migrate genera migraciones desde `schema.prisma`; no se editan manualmente.
- Selectores reutilizables con `select` e `include` cargan relaciones y producen tipos inferidos.
- Salidas, transferencias y órdenes usan `$transaction` con aislamiento `Serializable`.
- Las actualizaciones de saldo comparan `onHand` y `reserved` observados mediante `updateMany`.
- Un error `P2034` reintenta la transacción completa hasta tres veces; después se traduce a conflicto.
- Movimientos, auditoría e idempotencia se confirman junto con el cambio de negocio.

En el esquema inicial sin modelos, readiness crea un cliente Prisma aislado y abre una transacción interactiva vacía para forzar la autenticación y conectividad reales sin SQL raw. El cliente se desconecta al concluir la comprobación y la prueba tiene un límite de 1.5 segundos. La API no conecta PostgreSQL durante el arranque, por lo que liveness permanece disponible si la base está caída.

## Configuración

La configuración se valida al iniciar. Variables mínimas: `NODE_ENV`, `PORT`, `DATABASE_URL`, `JWT_ACCESS_SECRET`, `ACCESS_TOKEN_TTL`, `REFRESH_TOKEN_TTL`, `COOKIE_SECURE`, `COOKIE_SAME_SITE`, `WEB_ORIGIN` y `LOG_LEVEL`. Los secretos nunca tienen valores reales en el repositorio.

## Pruebas

- Unitarias para permisos, estados de orden, hashes y validadores.
- Integración con PostgreSQL real para tenant, relaciones, transacciones e idempotencia.
- Pruebas de repositorio aseguran que sólo se invoque Prisma Client y que no existan APIs raw.
- Supertest para contrato HTTP y cookies.
- Fixtures pequeñas y factorías; dataset separado para rendimiento.
