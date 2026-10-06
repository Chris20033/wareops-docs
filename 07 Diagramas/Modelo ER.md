# Modelo ER Maestro

Este diagrama muestra las 24 tablas persistentes en 3FN. Los atributos y claves aparecen en los diagramas por módulo.

```mermaid
erDiagram
    USER ||--o{ MEMBERSHIP : has
    USER ||--o{ REFRESH_SESSION : opens
    USER ||--o{ INVITATION : issues
    USER ||--o{ AUDIT_EVENT : acts
    ORGANIZATION ||--o{ MEMBERSHIP : contains
    ORGANIZATION ||--o{ INVITATION : receives
    ORGANIZATION ||--o{ BRANCH : owns
    ORGANIZATION ||--o{ PRODUCT : owns
    ORGANIZATION ||--o{ SUPPLIER : owns
    ORGANIZATION ||--o{ IDEMPOTENCY_RECORD : scopes
    ORGANIZATION ||--o{ AUDIT_EVENT : records
    ROLE ||--o{ MEMBERSHIP : assigns
    ROLE ||--o{ INVITATION : offers
    ROLE ||--o{ ROLE_PERMISSION : grants
    PERMISSION ||--o{ ROLE_PERMISSION : belongs
    BRANCH ||--o{ WAREHOUSE : contains
    PRODUCT ||--o{ PRODUCT_SUPPLIER : links
    SUPPLIER ||--o{ PRODUCT_SUPPLIER : links
    WAREHOUSE ||--o{ INVENTORY_BALANCE : holds
    PRODUCT ||--o{ INVENTORY_BALANCE : stocked
    MEMBERSHIP ||--o{ INVENTORY_OPERATION : performs
    INVENTORY_OPERATION ||--|{ INVENTORY_MOVEMENT : produces
    INVENTORY_BALANCE ||--o{ INVENTORY_MOVEMENT : receives
    INVENTORY_OPERATION ||--o| INVENTORY_ENTRY : specializes
    SUPPLIER ||--o{ INVENTORY_ENTRY : supplies
    INVENTORY_OPERATION ||--o| TRANSFER : describes
    INVENTORY_BALANCE ||--o{ TRANSFER : source
    INVENTORY_BALANCE ||--o{ TRANSFER : destination
    WAREHOUSE ||--o{ OUTBOUND_ORDER : fulfills
    MEMBERSHIP ||--o{ OUTBOUND_ORDER : creates
    OUTBOUND_ORDER ||--|{ OUTBOUND_ORDER_LINE : contains
    PRODUCT ||--o{ OUTBOUND_ORDER_LINE : requested
    OUTBOUND_ORDER ||--o{ OUTBOUND_ORDER_OPERATION : links
    INVENTORY_OPERATION ||--o| OUTBOUND_ORDER_OPERATION : links
    AUDIT_EVENT ||--o{ AUDIT_CHANGE : contains
```

## Diagramas detallados

- [[ER - Identidad y RBAC]]
- [[ER - Ubicaciones y Catálogo]]
- [[ER - Inventario y Transferencias]]
- [[ER - Órdenes y Reservas]]
- [[ER - Idempotencia y Auditoría]]

Véase [[../04 Base de Datos/Diccionario de Datos|Diccionario de datos]] y [[../04 Base de Datos/Normalización a Tercera Forma Normal|Normalización a 3FN]].
