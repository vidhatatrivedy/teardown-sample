# TASK-06-01-01 — Remove standalone enquiries router

**Epic:** EPIC-06  
**Feature:** FEAT-06-01 Tenant isolation fix  
**Size:** M  
**Priority:** Critical

## Dependencies

None — **start here**

## Context

Audit 07 F7.4 — `enquiries_standalone.router` at `/enquiries` duplicates scoped routes.

## Work

1. Grep frontend for `/enquiries` without restaurant prefix — update to scoped paths
2. Remove `enquiries_standalone` from `main.py`
3. Delete or archive standalone router file

## Acceptance criteria

- [ ] No API routes at `/enquiries` without restaurant_id in path
- [ ] Frontend enquiries page works via scoped API only
- [ ] OpenAPI docs show single enquiry surface
