# ER — Idempotencia y Auditoría

```mermaid
erDiagram
    ORGANIZATION {
        uuid id PK
    }
    USER {
        uuid id PK
    }
    IDEMPOTENCY_RECORD {
        uuid id PK
        uuid organization_id FK
        string key
        string request_hash
        string method
        string route
        int response_status
        json response_body
        string resource_type
        string resource_id
        datetime created_at
        datetime expires_at
    }
    AUDIT_EVENT {
        uuid id PK
        uuid organization_id FK
        uuid actor_user_id FK
        string action
        string entity_type
        uuid entity_id
        uuid request_id
        datetime created_at
    }
    AUDIT_CHANGE {
        uuid id PK
        uuid audit_event_id FK
        string field
        string old_value
        string new_value
    }
    ORGANIZATION ||--o{ IDEMPOTENCY_RECORD : scopes
    ORGANIZATION ||--o{ AUDIT_EVENT : records
    USER ||--o{ AUDIT_EVENT : acts
    AUDIT_EVENT ||--o{ AUDIT_CHANGE : contains
```

Claves compuestas: registro idempotente por organización/clave y cambio único por evento/campo. `responseBody` es un resultado técnico opaco; auditoría relacionaliza cada cambio.
