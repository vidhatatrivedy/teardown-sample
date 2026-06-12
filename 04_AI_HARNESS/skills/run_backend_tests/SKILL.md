# Skill — Run Backend Tests

Execute and add tests for Chef's Console FastAPI backend.

## Environment

```bash
cd backend
source venv/bin/activate   # REQUIRED
```

Never run Python from repo root without venv.

## Run all tests

```bash
pytest tests/ -v
```

## Run single file

```bash
pytest tests/test_tenant_isolation.py -v
```

## Test client pattern

`backend/tests/conftest.py`:

```python
import pytest
from httpx import AsyncClient, ASGITransport
from app.main import app

@pytest.fixture
async def client():
    transport = ASGITransport(app=app)
    async with AsyncClient(transport=transport, base_url="http://test") as ac:
        yield ac
```

## Auth helper

```python
async def get_token(client, email="test@example.com", password="[REDACTED]"):
    resp = await client.post("/auth/login", json={"email": email, "password": password})
    return resp.json()["access_token"]
```

## Tenant isolation test template

```python
async def test_cannot_access_other_restaurant_booking(client, restaurant_a, restaurant_b, token_a):
    booking_id = await create_booking_in_b(restaurant_b)
    resp = await client.get(
        f"/restaurants/{restaurant_a}/bookings/{booking_id}",
        headers={"Authorization": f"Bearer {token_a}"},
    )
    assert resp.status_code in (403, 404)
```

## Checklist

- [ ] Tests use isolated test database (env `TEST_MONGODB_URL`)
- [ ] No tests hit production MongoDB
- [ ] Async tests use `@pytest.mark.asyncio`
- [ ] Cleanup fixtures delete created documents

## Legacy scripts

Existing `backend/test_*.py` at repo root — migrate into `tests/` rather than extending ad-hoc scripts.
