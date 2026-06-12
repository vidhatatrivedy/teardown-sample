# TASK-05-04-01 — Backend subscription middleware

**Epic:** EPIC-05  
**Feature:** FEAT-05-04 Subscription gate  
**Size:** M  
**Priority:** High

## Dependencies

TASK-01-03-02

## Context

Frontend blocks dashboard; backend must return 403 on writes when `is_subscription_active=false`.

## Work

1. Create `require_active_subscription` dependency
2. Apply to all restaurant-scoped POST/PUT/PATCH/DELETE
3. GET routes may remain for read-only grace period (document choice)

## Acceptance criteria

- [ ] Inactive subscription → POST booking returns 403
- [ ] Admin activates → writes succeed without re-login
- [ ] Health and auth routes unaffected
