# TASK-05-02-01 — Team invitation accept flow

**Epic:** EPIC-05  
**Feature:** FEAT-05-02 Team invitations  
**Size:** M  
**Priority:** Medium

## Dependencies

TASK-05-01-01

## Context

Invite from restaurant management → email → `/invite/accept`.

## Work

1. Verify token expiry and single accept
2. New user sets password on accept if needed
3. Member appears in restaurant with assigned role

## Acceptance criteria

- [ ] Manager can invite staff email
- [ ] Accept adds user to `restaurant.members`
- [ ] Expired token shows error with re-invite instruction
