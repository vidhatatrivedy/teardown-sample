# TASK-02-01-01 — Enquiry CRUD on scoped restaurant routes

**Epic:** EPIC-02  
**Feature:** FEAT-02-01 Enquiry CRUD  
**Size:** M  
**Priority:** High

## Dependencies

TASK-06-01-01 (tenant isolation), TASK-05-03-01 (clients exist)

## Context

Use `/restaurants/{restaurant_id}/enquiries` only. Router: `backend/app/routers/enquiries.py`.

## Work

1. Verify all CRUD endpoints filter by `restaurant_id` from URL
2. Frontend `api.ts` uses scoped paths exclusively
3. Status transitions validated server-side

## Acceptance criteria

- [ ] Create/read/update/delete enquiry works from dashboard
- [ ] Enquiry from restaurant A not visible in restaurant B
- [ ] Invalid status transition returns 400
