# Flujos Críticos

## Inicio y renovación de sesión

```mermaid
sequenceDiagram
    actor U as Usuario
    participant W as Web
    participant A as API (/api/v1)
    participant D as PostgreSQL
    U->>W: Registro o inicio de sesión
    W->>A: POST /auth/register o POST /auth/login
    A->>D: Verificar Argon2id / crear User + Organization + Membership(OWNER) + RefreshSession(tokenHash)
    A-->>W: 201/200 { data: { accessToken, user, organizations } } + Set-Cookie HttpOnly (wareops_refresh_token)
    W->>A: Solicitud protegida con Bearer JWT + X-Organization-Id
    A->>D: Verificar RefreshSession vigente + Membership ACTIVE + RolePermission
    A-->>W: Respuesta aislada al tenant activo
    W->>A: POST /auth/refresh (Cookie HttpOnly + Origin permitido)
    A->>D: Validar sessionId/tokenHash; si reutiliza token rotado revoca sesión; si válido rota tokenHash
    A-->>W: 200 Nuevo accessToken + nueva Cookie HttpOnly
    W->>A: POST /auth/logout (Bearer JWT)
    A->>D: Marcar RefreshSession.revokedAt y limpiar Cookie
    A-->>W: 200 { data: { loggedOut: true } }
```

## Operación idempotente de inventario

```mermaid
sequenceDiagram
    participant W as Web
    participant A as API
    participant D as PostgreSQL
    W->>A: POST comando + Idempotency-Key
    A->>D: Prisma $transaction Serializable
    A->>D: Leer clave y saldo mediante Prisma Client
    A->>A: Validar tenant, activos e invariantes
    alt válido
        A->>D: updateMany comparando saldo observado
        A->>D: Crear operación + movimiento + auditoría
        A->>D: Guardar respuesta y COMMIT
        A-->>W: Resultado
    else conflicto P2034
        A->>D: ROLLBACK
        A->>A: Reintentar hasta 3 veces
    else inválido
        A->>D: ROLLBACK
        A-->>W: Error estable
    end
```

## Transferencia

```mermaid
sequenceDiagram
    participant A as API
    participant D as PostgreSQL
    A->>D: Prisma $transaction Serializable
    A->>D: Leer origen y destino con relaciones
    A->>A: Validar disponibilidad y almacenes
    A->>D: updateMany con valores observados
    A->>D: Crear operación, transferencia y movimientos
    A->>D: Insertar auditoría/idempotencia y COMMIT
```

## Ciclo de orden

```mermaid
stateDiagram-v2
    [*] --> DRAFT
    DRAFT --> CONFIRMED: confirmar / reservar todo
    CONFIRMED --> COMPLETED: completar / consumir reserva
    CONFIRMED --> CANCELLED: cancelar / liberar reserva
    DRAFT --> CANCELLED: cancelar borrador
    COMPLETED --> [*]
    CANCELLED --> [*]
```
