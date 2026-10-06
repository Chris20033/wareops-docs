# Despliegue

## Estrategia

Frontend, API y PostgreSQL se despliegan independientemente. La documentación no fija proveedor: cualquier opción debe ofrecer HTTPS, variables seguras, logs, backups de base de datos y una región compatible.

## Entorno local

Docker Compose levanta API y PostgreSQL; la web puede ejecutarse en contenedor o con Node local. El flujo documentado deberá incluir instalación, migración, seed, arranque, pruebas y limpieza segura.

Desde `wareops-api`, `docker compose up --build -d` construye la API y levanta PostgreSQL 18 con un volumen persistente. `docker compose down` detiene los servicios sin borrar datos; `docker compose down -v` también elimina la base local y debe ejecutarse sólo de forma deliberada. El README de la API mantiene los comandos completos de instalación, Prisma, pruebas y operación.

## Artefactos

- Imagen API multi-stage, usuario no root, sólo dependencias de producción y health check.
- Build optimizado de Next.js, preferentemente salida standalone si el proveedor usa contenedor.
- Migraciones generadas por Prisma Migrate y ejecutadas como paso único previo al arranque de la nueva API, nunca editadas manualmente ni lanzadas desde varias réplicas.

## CI

Cada repositorio ejecuta instalación reproducible, lint, pruebas y build. La API añade una base PostgreSQL efímera para integración y verifica migraciones. La web instala navegadores sólo en el job E2E.

## Salud y observabilidad

- `/health/live`: proceso iniciado.
- `/health/ready`: conexión esencial con PostgreSQL disponible.
- `/docs`: Swagger UI; `/docs-json`: contrato OpenAPI serializado.
- Logs JSON con timestamp, nivel, servicio, entorno, `requestId`, ruta, estado y duración.
- No se registran cuerpos completos por defecto.

## Configuración y despliegue

Los entornos `development`, `test` y `demo` usan secretos separados. CORS, cookies, URL de API y HTTPS se validan después del despliegue. El seed de demo crea datos ficticios y credenciales documentadas fuera del código productivo.

## Recuperación

Antes de una migración incompatible se exige backup y prueba de restauración del proveedor elegido. El rollback de aplicación sólo es válido si sigue siendo compatible con el esquema ya migrado.
