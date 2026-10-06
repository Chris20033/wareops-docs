# ER — Inventario y Transferencias

```mermaid
erDiagram
    MEMBERSHIP {
        uuid id PK
    }
    WAREHOUSE {
        uuid id PK
    }
    PRODUCT {
        uuid id PK
    }
    SUPPLIER {
        uuid id PK
    }
    INVENTORY_BALANCE {
        uuid id PK
        uuid warehouse_id FK
        uuid product_id FK
        int on_hand
        int reserved
        int minimum_stock
        datetime created_at
        datetime updated_at
    }
    INVENTORY_OPERATION {
        uuid id PK
        uuid actor_membership_id FK
        string type
        string reason
        string external_reference
        datetime created_at
    }
    INVENTORY_MOVEMENT {
        uuid id PK
        uuid operation_id FK
        uuid balance_id FK
        int on_hand_delta
        int reserved_delta
    }
    INVENTORY_ENTRY {
        uuid operation_id PK, FK
        uuid supplier_id FK
    }
    TRANSFER {
        uuid id PK
        uuid operation_id FK, UK
        uuid source_balance_id FK
        uuid destination_balance_id FK
        int quantity
    }
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
```

Claves compuestas: `InventoryBalance(warehouseId, productId)` e `InventoryMovement(operationId, balanceId)`. Producto, almacenes, membresía y proveedor deben resolver al mismo tenant antes de escribir.
