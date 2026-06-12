# Skill — Add API Endpoint

Add a new REST endpoint to Chef's Console backend following project conventions.

## When to use

Adding CRUD or action endpoint under `/restaurants/{restaurant_id}/...`

## Prerequisites

- Read [rbac_access_control.md](../../02_BUILD_SPEC/rbac_access_control.md)
- Identify required `Permission` enum value

## Steps

### 1. Pydantic models (if new shapes)

File: `backend/app/models/{entity}.py`

```python
class ThingCreate(BaseModel):
    name: str

class ThingResponse(BaseModel):
    id: str
    name: str
    restaurant_id: str
```

### 2. Router handler

File: `backend/app/routers/{entity}.py`

```python
@router.post("/", response_model=ThingResponse)
async def create_thing(
    restaurant_id: str,
    data: ThingCreate,
    current_user: User = Depends(get_current_user_from_token),
    _: None = Depends(require_permission(Permission.CREATE_THINGS)),
):
    await verify_restaurant_access(restaurant_id, current_user)
    thing = Thing(**data.model_dump(), restaurant_id=restaurant_id, created_by=str(current_user.id))
    await thing.insert()
    return ThingResponse(id=str(thing.id), ...)
```

### 3. Register router (if new file)

`backend/app/main.py` — only if new router module; prefer existing domain router.

### 4. Frontend api.ts method

```typescript
async createThing(restaurantId: string, data: ThingCreate): Promise<Thing> {
  return this.request(`/restaurants/${restaurantId}/things`, {
    method: 'POST',
    body: JSON.stringify(data),
  });
}
```

### 5. Test

```python
async def test_create_thing_requires_auth(client):
    resp = await client.post(f"/restaurants/{rid}/things", json={...})
    assert resp.status_code == 401
```

## Checklist

- [ ] Permission dependency on mutating routes
- [ ] `restaurant_id` in every DB query
- [ ] Response model typed
- [ ] OpenAPI shows new endpoint at `/docs`

## Do not

- Add routes to `enquiries_standalone` pattern
- Use `Thing.get(id)` without restaurant filter
- Skip subscription check on writes (when middleware exists)
