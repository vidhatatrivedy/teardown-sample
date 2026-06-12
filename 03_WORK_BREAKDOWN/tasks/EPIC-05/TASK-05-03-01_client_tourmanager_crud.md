# TASK-05-03-01 — Client CRUD with tour managers

**Epic:** EPIC-05  
**Feature:** FEAT-05-03 Client & tour manager CRUD  
**Size:** M  
**Priority:** High

## Dependencies

TASK-05-01-01

## Context

`/dashboard/clients` — `clients.py`, `tourmanagers.py` routers.

## Work

1. Client form with billing/delivery nested fields
2. Tour manager sub-CRUD under client detail
3. Deactivate client (`is_active=false`) instead of hard delete if bookings exist

## Acceptance criteria

- [ ] Create client "Acme Catering Ltd" with default pricing
- [ ] Add tour manager under client
- [ ] Client list scoped to selected restaurant only
