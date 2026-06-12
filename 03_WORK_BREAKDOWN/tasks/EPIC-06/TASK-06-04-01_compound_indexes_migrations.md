# TASK-06-04-01 — Add compound indexes and migration scripts

**Epic:** EPIC-06  
**Feature:** FEAT-06-04 Database indexes & migrations  
**Size:** M  
**Priority:** Medium

## Dependencies

None

## Context

[database_schema.md](../../../02_BUILD_SPEC/database_schema.md) recommended indexes.

## Work

1. Create `backend/migrations/001_add_compound_indexes.py`
2. Add indexes to Beanie model Settings where supported
3. Document run procedure in migration README

## Acceptance criteria

- [ ] Indexes exist on bookings, enquiries, orders for restaurant_id + date
- [ ] Unique index on (restaurant_id, booking_reference) for bookings
- [ ] Migration script idempotent (safe to run twice)
