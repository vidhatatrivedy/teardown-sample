# TASK-03-01-01 — Bookings list with batch-populate optimization

**Epic:** EPIC-03  
**Feature:** FEAT-03-01 Booking table & CRUD  
**Size:** L  
**Priority:** High

## Dependencies

TASK-02-03-01

## Context

`bookings.py` list endpoint enriches each row with enquiry/client — N+1 risk per Audit 05.

## Work

1. Refactor populate to batch-fetch enquiries and clients by ID set
2. Maintain `BookingResponse` shape for frontend
3. Add pagination params `skip`, `limit` default 50

## Acceptance criteria

- [ ] 100 bookings list in under 500ms p95 on dev hardware
- [ ] Inline edit updates single booking
- [ ] Mongo query count ≤ 3 per list request
