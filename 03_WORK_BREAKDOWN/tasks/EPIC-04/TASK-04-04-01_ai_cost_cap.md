# TASK-04-04-01 — AI daily cost cap per restaurant

**Epic:** EPIC-04  
**Feature:** FEAT-04-04 AI guardrails  
**Size:** M  
**Priority:** High

## Dependencies

TASK-02-02-01

## Context

Audit 08 — no rate/cost limits on AI calls.

## Work

1. Track token usage per restaurant per day in MongoDB counter
2. Reject extraction with 429 when over cap (configurable default: 100 requests/day)
3. Admin override flag on restaurant settings (optional)

## Acceptance criteria

- [ ] 101st extraction in same day returns 429 with clear message
- [ ] Counter resets at UTC midnight
- [ ] Usage visible in dashboard settings (read-only)
