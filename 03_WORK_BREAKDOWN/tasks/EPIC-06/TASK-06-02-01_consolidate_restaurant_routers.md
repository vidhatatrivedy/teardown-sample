# TASK-06-02-01 — Consolidate restaurant routers

**Epic:** EPIC-06  
**Feature:** FEAT-06-02 Router consolidation  
**Size:** M  
**Priority:** Medium

## Dependencies

TASK-06-01-01

## Context

`restaurants.py` + `restaurants_enhanced.py` both mounted in `main.py`.

## Work

1. Merge enhanced endpoints into single router module
2. Deprecation headers on old paths if URLs change (prefer no URL change)
3. Update frontend if any path differences

## Acceptance criteria

- [ ] Single `restaurants` router module
- [ ] All existing restaurant API tests/clients still work
- [ ] No duplicate route definitions in OpenAPI
