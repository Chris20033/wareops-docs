# Requisitos No Funcionales

## Seguridad

- **RNF-001:** Las contraseñas se almacenarán exclusivamente como hashes Argon2id con parámetros vigentes y documentados.
- **RNF-002:** Los refresh tokens se almacenarán de forma revocable y no se persistirán en texto plano.
- **RNF-003:** Toda consulta de negocio incluirá el contexto de organización validado por el servidor.
- **RNF-004:** La aplicación no expondrá secretos ni tokens en repositorios, logs o respuestas de error.
- **RNF-005:** Los datos de entrada se validarán en el límite de la API y en formularios web.

## Consistencia y confiabilidad

- **RNF-006:** Las operaciones que afectan varias filas de inventario usarán transacciones de base de datos.
- **RNF-007:** Bajo solicitudes concurrentes, sólo podrán confirmarse consumos cuya disponibilidad haya sido reservada o comprobada atómicamente.
- **RNF-008:** La repetición de un comando con la misma clave de idempotencia y carga no producirá movimientos adicionales.
- **RNF-009:** Una misma clave de idempotencia con una carga diferente será rechazada con conflicto.

## Rendimiento

- **RNF-010:** En el entorno de demostración, el percentil 95 de lecturas paginadas comunes deberá ser menor a 500 ms con hasta 100 000 movimientos precargados, excluyendo latencia de red pública.
- **RNF-011:** Los listados devolverán como máximo 100 registros por página y usarán índices para filtros frecuentes.
- **RNF-012:** El dashboard deberá cargar sus indicadores principales en menos de 2 segundos en el entorno de demostración.

## Calidad y mantenibilidad

- **RNF-013:** API y web usarán TypeScript con modo estricto.
- **RNF-014:** Cada repositorio ejecutará lint, pruebas y build en GitHub Actions.
- **RNF-015:** Las reglas críticas de inventario, aislamiento y autorización tendrán pruebas automatizadas.
- **RNF-016:** Las decisiones arquitectónicas relevantes se registrarán en ADR.
- **RNF-017:** La API publicará una especificación OpenAPI sincronizada con los controladores.

## Usabilidad y accesibilidad

- **RNF-018:** La interfaz será utilizable en escritorio y tablet; las operaciones críticas también serán accesibles en móvil.
- **RNF-019:** Formularios y controles principales serán operables con teclado, tendrán etiquetas accesibles y contraste equivalente a WCAG 2.1 AA.
- **RNF-020:** Los errores mostrarán una explicación accionable sin revelar información interna.

## Operación

- **RNF-021:** API, PostgreSQL y servicios auxiliares del desarrollo podrán iniciarse con Docker Compose.
- **RNF-022:** La API emitirá logs estructurados con identificador de solicitud, sin datos sensibles.
- **RNF-023:** El endpoint de salud distinguirá disponibilidad del proceso y acceso a dependencias esenciales.
- **RNF-024:** Las fechas se persistirán en UTC y se presentarán según la zona horaria configurada.

> Estas metas son criterios de ingeniería para el proyecto de portafolio, no un acuerdo de nivel de servicio comercial.
