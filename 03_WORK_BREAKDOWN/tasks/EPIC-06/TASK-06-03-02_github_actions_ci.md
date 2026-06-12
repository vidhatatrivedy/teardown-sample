# TASK-06-03-02 — GitHub Actions CI pipeline

**Epic:** EPIC-06  
**Feature:** FEAT-06-03  
**Size:** M  
**Priority:** High

## Dependencies

TASK-06-03-01

## Context

No CI visible in repo — add PR gate.

## Work

1. `.github/workflows/backend-tests.yml` — pytest on PR
2. Optional: frontend `npm run lint` job
3. Mongo service container in CI

## Acceptance criteria

- [ ] PR to main runs pytest automatically
- [ ] Failed tests block merge
- [ ] README badge optional
