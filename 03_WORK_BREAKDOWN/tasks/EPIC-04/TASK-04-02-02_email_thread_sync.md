# TASK-04-02-02 — Email thread sync and storage

**Epic:** EPIC-04  
**Feature:** FEAT-04-02  
**Size:** M  
**Priority:** Medium

## Dependencies

TASK-04-02-01

## Context

`EmailThread`, `EmailMessage` models; processing in `email_processing_service.py`.

## Work

1. Verify idempotent upsert by `message_id`
2. Processing status transitions: pending → processed → failed
3. Log sync count per integration per cycle

## Acceptance criteria

- [ ] New inbox email appears in DB within 2 poll cycles
- [ ] Duplicate poll does not duplicate messages
- [ ] Failed processing sets status with error reason
