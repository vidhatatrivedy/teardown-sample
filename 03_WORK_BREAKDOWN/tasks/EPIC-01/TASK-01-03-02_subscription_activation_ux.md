# TASK-01-03-02 — Subscription activation waiting page UX

**Epic:** EPIC-01  
**Feature:** FEAT-01-03  
**Size:** S  
**Priority:** Medium

## Dependencies

TASK-01-03-01

## Context

`/subscription-activation` blocks dashboard until admin activates subscription.

## Work

1. Clear copy: what happened, what to do, support contact
2. Poll or manual refresh when subscription becomes active
3. Link to admin process (internal doc only)

## Acceptance criteria

- [ ] Page explains subscription is pending admin activation
- [ ] When `is_subscription_active` becomes true, user reaches dashboard on navigation
- [ ] No dead-end without support contact info
