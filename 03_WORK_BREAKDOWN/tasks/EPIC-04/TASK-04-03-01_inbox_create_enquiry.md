# TASK-04-03-01 — Email inbox UI create enquiry action

**Epic:** EPIC-04  
**Feature:** FEAT-04-03 Email inbox UI  
**Size:** M  
**Priority:** Medium

## Dependencies

TASK-04-02-02, TASK-02-02-01

## Context

`/dashboard/email-processing` — thread view with create enquiry from extracted data.

## Work

1. Thread detail shows AI extracted fields when present
2. "Create enquiry" pre-fills form from thread
3. Link thread to created enquiry_id (metadata field if needed)

## Acceptance criteria

- [ ] Staff creates enquiry from email thread in under 2 minutes
- [ ] Created enquiry linked to correct restaurant
- [ ] Low confidence extraction shows warning banner
