# Glosario

| Término | Definición |
| --- | --- |
| Organización | Empresa aislada dentro de WareOps. Es el límite principal de acceso a datos. |
| Sucursal | Unidad operativa o ubicación comercial de una organización. |
| Almacén | Ubicación física, perteneciente a una sucursal, donde se mantiene inventario. |
| Existencia física | Unidades registradas actualmente en un almacén (`onHand`). |
| Existencia reservada | Unidades apartadas para órdenes confirmadas (`reserved`). |
| Existencia disponible | Unidades utilizables: `onHand - reserved`. |
| Saldo de inventario | Estado actual de existencia física, reservada y mínimo para un producto en un almacén. |
| SKU | Código de producto único dentro de una organización. |
| Movimiento | Registro inmutable de un cambio de existencia. |
| Transferencia | Operación atómica que descuenta unidades de un almacén y las agrega a otro. |
| Ajuste | Corrección positiva o negativa justificada de inventario. |
| Orden de salida | Solicitud interna que reserva productos y posteriormente genera su salida. |
| Membresía | Asociación de un usuario con una organización y un rol. |
| Tenant | Organización cuyos datos deben permanecer aislados. |
| Idempotencia | Propiedad que permite repetir una solicitud sin duplicar su efecto. |
| Clave de idempotencia | Identificador aportado por el cliente para reconocer reintentos del mismo comando. |
| Access token | JWT de corta duración usado para autenticar solicitudes. |
| Refresh token | Secreto opaco y rotatorio que permite obtener un nuevo access token. |
| Organización activa | Organización indicada por la web para una solicitud y validada por la API contra las membresías del usuario. |
| Auditoría | Registro de quién realizó una acción, cuándo y sobre qué datos. |
| 3FN | Tercera forma normal: cada atributo no clave depende de la clave, de toda la clave y no de otro atributo no clave. |
| Selector Prisma | Objeto reutilizable de `select` o `include` que define relaciones y campos de una consulta tipada. |
| MVP | Conjunto mínimo de capacidades que constituye una demostración completa y funcional. |
