# TASK-03-02-01 — Bulk booking payment status update

**Epic:** EPIC-03  
**Feature:** FEAT-03-02 Bulk booking updates  
**Size:** M  
**Priority:** Medium

## Dependencies

TASK-03-01-01

## Context

Ops managers bulk-update payment status before delivery day. Endpoint: `POST .../bookings/bulk/update-payment-status`.

## Work

1. Verify permission `manage_bookings`
2. UI: multi-select rows + payment status dropdown
3. Toast with count updated

## Acceptance criteria

- [ ] 30 bookings updated to `paid` in one action
- [ ] Staff role without permission sees disabled bulk action
- [ ] Audit log entry (optional future — document as out of scope)
