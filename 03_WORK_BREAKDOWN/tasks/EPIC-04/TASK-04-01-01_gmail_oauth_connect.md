# TASK-04-01-01 — Gmail OAuth connect flow

**Epic:** EPIC-04  
**Feature:** FEAT-04-01 OAuth email connect  
**Size:** M  
**Priority:** High

## Dependencies

TASK-01-03-01

## Context

`email_integration.py` — OAuth authorize + callback stores tokens in `EmailIntegration`.

## Work

1. Verify redirect URIs match env config
2. Store refresh token securely (encrypt — ties TASK-06-05-01)
3. Settings UI shows connected account + disconnect

## Acceptance criteria

- [ ] User completes Gmail OAuth from settings
- [ ] Integration shows status `active`
- [ ] Disconnect removes tokens and stops polling
