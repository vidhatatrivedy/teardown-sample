# TASK-06-05-01 — Fix DEBUG exception handler and encrypt OAuth tokens

**Epic:** EPIC-06  
**Feature:** FEAT-06-05 Security hardening  
**Size:** M  
**Priority:** Critical

## Dependencies

None — **Week 1**

## Context

Audit 06 F6.1 DEBUG leak; F6.3 OAuth tokens plaintext in MongoDB.

## Work

1. Change global exception handler to never return `str(exc)` to client
2. Add `encrypt_token()` / `decrypt_token()` util using Fernet key from env
3. Migrate existing EmailIntegration tokens on deploy

## Acceptance criteria

- [ ] Forced 500 in DEBUG mode returns generic message only
- [ ] OAuth tokens stored encrypted in MongoDB
- [ ] Email sync still works after migration
