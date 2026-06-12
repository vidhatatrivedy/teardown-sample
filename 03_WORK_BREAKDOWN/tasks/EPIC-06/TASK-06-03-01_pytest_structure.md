# TASK-06-03-01 — pytest structure and core tests

**Epic:** EPIC-06  
**Feature:** FEAT-06-03 Test suite & CI  
**Size:** L  
**Priority:** High

## Dependencies

None

## Context

Ad-hoc test scripts in repo root — migrate to `backend/tests/`.

## Work

1. Add `pytest`, `pytest-asyncio`, `httpx` test client setup
2. Migrate auth login test from `test_api.py`
3. Add conftest with test DB fixture (Mongo memory or test database)

## Acceptance criteria

- [ ] `pytest` runs from `backend/` with venv active
- [ ] Minimum 15 tests covering auth, enquiries, bookings
- [ ] Tests isolated — no production DB
