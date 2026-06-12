# TASK-02-03-01 — Atomic enquiry → booking + order conversion

**Epic:** EPIC-02  
**Feature:** FEAT-02-03 Enquiry conversion  
**Size:** L  
**Priority:** Critical

## Dependencies

TASK-02-01-01, TASK-03-01-01

## Context

`POST /restaurants/{id}/enquiries/{eid}/convert` must create Booking and Order with shared `booking_reference`. See [system_design.md](../../../02_BUILD_SPEC/system_design.md).

## Work

1. Audit convert handler for transaction-like behavior (Mongo session if needed)
2. Set enquiry status to `approved`
3. Populate booking from enquiry + client defaults
4. Create order with at least one line item from total

## Acceptance criteria

- [ ] Convert returns booking_id and order_id
- [ ] All three entities share same `booking_reference`
- [ ] Partial failure rolls back — no orphan booking without order
- [ ] pytest integration test for convert
