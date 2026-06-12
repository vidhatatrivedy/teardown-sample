# TASK-02-04-01 — Bulk enquiry status update

**Epic:** EPIC-02  
**Feature:** FEAT-02-04 Bulk enquiry ops  
**Size:** S  
**Priority:** Low

## Dependencies

TASK-02-01-01

## Context

`POST .../enquiries/bulk/update-status` — used rarely but must not timeout.

## Work

1. Cap batch size at 100 IDs
2. Return partial success report if some IDs invalid
3. Frontend checkbox selection + bulk action bar

## Acceptance criteria

- [ ] 50 enquiries updated in one request
- [ ] Invalid ID in batch returns 207 or clear error list
- [ ] Permission `manage_enquiries` required
