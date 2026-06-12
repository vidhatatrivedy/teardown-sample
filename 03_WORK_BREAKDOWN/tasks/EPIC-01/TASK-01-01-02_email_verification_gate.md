# TASK-01-01-02 — Email verification gate before dashboard

**Epic:** EPIC-01  
**Feature:** FEAT-01-01  
**Size:** S  
**Priority:** Medium

## Dependencies

TASK-01-01-01

## Context

Signup sends verification email. `is_verified` on User must gate dashboard access consistently on frontend and backend.

## Work

1. Verify `AuthWrapper` blocks unverified users to `/verify-email`
2. Backend: return 403 on mutating routes if `not user.is_verified`
3. Resend verification endpoint rate-limited (ties to EPIC-06)

## Acceptance criteria

- [ ] Unverified user cannot access `/dashboard/*`
- [ ] Verified user proceeds to onboarding or dashboard
- [ ] Resend verification shows success toast (no email enumeration leak in message)
