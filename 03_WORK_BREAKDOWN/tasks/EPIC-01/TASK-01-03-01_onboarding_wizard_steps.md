# TASK-01-03-01 — Onboarding wizard step completion tracking

**Epic:** EPIC-01  
**Feature:** FEAT-01-03 Onboarding wizard  
**Size:** M  
**Priority:** High

## Dependencies

TASK-01-01-02

## Context

`/onboarding` page guides restaurant creation. User flags: `onboarding_completed`, `restaurant_created`, `email_integrated`.

## Work

1. Map each wizard step to API calls in `onboarding.py`
2. Ensure flags update atomically after restaurant create
3. Redirect to subscription-activation if subscription inactive

## Acceptance criteria

- [ ] Completing wizard sets `onboarding_completed=true`
- [ ] User cannot skip restaurant creation step
- [ ] Refresh mid-wizard resumes at correct step
