# TASK-01-02-01 — Google OAuth callback and account linking

**Epic:** EPIC-01  
**Feature:** FEAT-01-02 Google OAuth  
**Size:** M  
**Priority:** Medium

## Dependencies

TASK-01-01-01

## Context

Routes in `backend/app/routers/google_auth.py`, frontend `/auth/google/callback`. Handle new user vs existing email account merge.

## Work

1. Document OAuth scopes requested
2. Verify `google_id` stored; `auth_provider` set correctly
3. Edge case: Google email matches existing password account — define behavior
4. Test callback with mock Google token in pytest

## Acceptance criteria

- [ ] New Google user creates account and receives JWT
- [ ] Returning Google user logs in
- [ ] Callback errors show user-friendly message on `/login`
