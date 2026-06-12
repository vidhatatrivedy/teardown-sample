# TASK-06-01-02 — Cross-tenant integration tests

**Epic:** EPIC-06  
**Feature:** FEAT-06-01  
**Size:** L  
**Priority:** Critical

## Dependencies

TASK-06-01-01

## Context

[rbac_access_control.md](../../../02_BUILD_SPEC/rbac_access_control.md) tenant isolation test matrix.

## Work

1. Create `backend/tests/test_tenant_isolation.py`
2. Fixtures: two restaurants, two users
3. Tests: cross-restaurant GET/PUT/DELETE → 403

## Acceptance criteria

- [ ] 10+ isolation tests pass in CI
- [ ] Booking IDOR attempt fails
- [ ] Enquiry list never returns other tenant data
