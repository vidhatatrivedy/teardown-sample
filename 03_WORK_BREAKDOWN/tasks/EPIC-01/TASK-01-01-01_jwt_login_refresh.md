# TASK-01-01-01 — Verify and harden JWT login/refresh flow

**Epic:** EPIC-01 Auth & Onboarding  
**Feature:** FEAT-01-01 JWT authentication  
**Size:** M  
**Priority:** High

## Dependencies

None

## Context

Auth implemented in `backend/app/routers/auth.py` and `frontend/src/lib/unified-auth-context.tsx`. Verify token expiry, refresh rotation, and 401 retry logic match [api_reference.md](../../../02_BUILD_SPEC/api_reference.md).

## Work

1. Audit access/refresh token TTL in `config.py`
2. Ensure refresh invalidates old token (or document accepted risk)
3. Frontend: verify single-flight refresh on concurrent 401s
4. Add test: login → access protected route → expire token → refresh → succeed

## Acceptance criteria

- [ ] Login returns access + refresh tokens
- [ ] Expired access token triggers refresh without user re-login
- [ ] Invalid refresh returns 401 and clears frontend auth state
- [ ] pytest covers login and refresh happy path

## Spec links

- [system_design.md — Authentication](../../../02_BUILD_SPEC/system_design.md)
