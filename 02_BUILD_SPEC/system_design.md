# System Design

## Component diagram

```mermaid
flowchart TB
    subgraph frontend [Frontend]
        AuthCtx[AuthProvider]
        RestCtx[RestaurantProvider]
        Pages[App Router pages]
        ApiClient[api.ts]
    end
    subgraph backend [Backend]
        Routers[FastAPI routers]
        Perms[permissions.py]
        AuthUtil[auth utils]
        EmailSvc[email_processing_service]
        AISvc[ai_extraction_service]
        BgMgr[background_task_manager]
    end
    subgraph models [Models]
        UserM[User]
        RestM[Restaurant]
        EnqM[Enquiry]
        BookM[Booking]
        OrdM[Order]
        ClientM[Client]
        EmailM[EmailIntegration]
    end
    Pages --> AuthCtx
    Pages --> RestCtx
    Pages --> ApiClient
    ApiClient --> Routers
    Routers --> Perms
    Routers --> AuthUtil
    Routers --> models
    Routers --> AISvc
    BgMgr --> EmailSvc
    EmailSvc --> AISvc
    EmailSvc --> EnqM
```

## Sequence: Authentication

```mermaid
sequenceDiagram
    participant FE as Frontend
    participant API as POST /auth/login
    participant DB as MongoDB
    FE->>API: email + password
    API->>DB: find User by email
    API->>API: verify bcrypt hash
    API->>API: create access + refresh JWT
    API-->>FE: tokens + user object
    FE->>FE: store tokens localStorage
    FE->>API: GET /auth/me (Bearer)
    API-->>FE: UserResponse
```

## Sequence: Enquiry conversion

```mermaid
sequenceDiagram
    participant User as Staff
    participant API as enquiries router
    participant DB as MongoDB
    User->>API: POST /restaurants/{rid}/enquiries/{eid}/convert
    API->>API: require_permission CREATE_BOOKINGS
    API->>DB: fetch Enquiry + Client
    API->>DB: create Booking
    API->>DB: create Order with items
    API->>DB: update Enquiry status approved
    API-->>User: booking + order response
```

**Invariants:**
- `booking_reference` identical across enquiry, booking, order
- `enquiry_id` set on booking and order
- `restaurant_id` on all three matches URL path

## Sequence: Email background processing

```mermaid
sequenceDiagram
    participant Bg as BackgroundTaskManager
    participant Int as EmailIntegration
    participant Svc as EmailProcessingService
    participant AI as AIExtractionService
    participant DB as MongoDB
    loop Every poll interval
        Bg->>Int: list active integrations
        Bg->>Svc: fetch new messages
        Svc->>AI: classify and extract
        AI-->>Svc: entities + confidence
        Svc->>DB: upsert EmailThread/Message
    end
```

**Note:** Staff explicitly creates enquiry from inbox — no auto-convert without user action.

## Sequence: Permission check

```mermaid
sequenceDiagram
    participant R as Router handler
    participant P as permissions.py
    participant DB as MongoDB
    R->>P: require_permission(MANAGE_BOOKINGS)
    P->>DB: load Restaurant + members
    P->>P: resolve user role in restaurant
    P->>P: check ROLE_PERMISSIONS map
    alt denied
        P-->>R: HTTP 403
    else allowed
        P-->>R: continue handler
    end
```

## Data flow: enquiry pipeline

```mermaid
flowchart LR
    Email[Email thread] --> Extract[AI extraction]
    Manual[Manual form] --> Enquiry
    Extract --> Enquiry
    Enquiry -->|convert| Booking
    Enquiry -->|convert| Order
    Client --> Enquiry
    TourMgr[TourManager] --> Enquiry
```

## Error handling convention

| HTTP | Meaning | Response shape |
|------|---------|----------------|
| 400 | Validation error | `{ "detail": "..." }` |
| 401 | Missing/invalid JWT | `{ "detail": "Not authenticated" }` |
| 403 | Permission or subscription denied | `{ "detail": "..." }` |
| 404 | Resource not found or wrong tenant | `{ "detail": "..." }` |
| 422 | Pydantic validation | `{ "detail": [...] }` |
| 500 | Server error | `{ "detail": "Internal server error" }` (no stack in prod)

## Single points of failure

| SPOF | Mitigation target |
|------|-------------------|
| API process hosts background jobs | Separate worker |
| Single MongoDB instance | Atlas replica set |
| Shared OpenAI API key | Per-tenant limits + monitoring |
