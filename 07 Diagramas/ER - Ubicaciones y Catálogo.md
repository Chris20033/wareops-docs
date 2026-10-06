# ER — Ubicaciones y Catálogo

```mermaid
erDiagram
    ORGANIZATION {
        uuid id PK
        string name
    }
    BRANCH {
        uuid id PK
        uuid organization_id FK
        string code
        string name
        string address
        boolean is_active
        datetime created_at
        datetime updated_at
    }
    WAREHOUSE {
        uuid id PK
        uuid branch_id FK
        string code
        string name
        string description
        boolean is_active
        datetime created_at
        datetime updated_at
    }
    PRODUCT {
        uuid id PK
        uuid organization_id FK
        string sku
        string name
        string description
        boolean is_active
        datetime created_at
        datetime updated_at
    }
    SUPPLIER {
        uuid id PK
        uuid organization_id FK
        string code
        string name
        string contact_name
        string email
        string phone
        boolean is_active
        datetime created_at
        datetime updated_at
    }
    PRODUCT_SUPPLIER {
        uuid product_id PK, FK
        uuid supplier_id PK, FK
        datetime created_at
    }
    ORGANIZATION ||--o{ BRANCH : owns
    BRANCH ||--o{ WAREHOUSE : contains
    ORGANIZATION ||--o{ PRODUCT : owns
    ORGANIZATION ||--o{ SUPPLIER : owns
    PRODUCT ||--o{ PRODUCT_SUPPLIER : links
    SUPPLIER ||--o{ PRODUCT_SUPPLIER : links
```

Claves compuestas: sucursal por organización/código, almacén por sucursal/código, producto por organización/SKU, proveedor por organización/código y producto–proveedor.
