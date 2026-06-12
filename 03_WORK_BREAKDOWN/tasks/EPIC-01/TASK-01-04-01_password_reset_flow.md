# TASK-01-04-01 — Password reset end-to-end

**Epic:** EPIC-01  
**Feature:** FEAT-01-04 Password recovery  
**Size:** M  
**Priority:** Medium

## Dependencies

TASK-01-01-01

## Context

Forgot password → email token → `/reset-password`. Models: `PasswordResetToken`.

## Work

1. Verify token expiry enforced
2. Token single-use after reset
3. Frontend forms wired to API with validation

## Acceptance criteria

- [ ] Reset email sent for valid email (same response for invalid — no enumeration)
- [ ] Expired token shows error with link to request new
- [ ] Successful reset allows login with new password
