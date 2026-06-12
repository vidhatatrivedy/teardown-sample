# TASK-05-01-01 — Audit all routes for require_permission

**Epic:** EPIC-05  
**Feature:** FEAT-05-01 Role permission enforcement  
**Size:** L  
**Priority:** Critical

## Dependencies

None (start Week 1)

## Context

[rbac_access_control.md](../../../02_BUILD_SPEC/rbac_access_control.md) — every mutating route needs `require_permission`.

## Work

1. Script or manual audit of all 18 router files
2. Add missing permission dependencies
3. Document matrix route → permission in build spec appendix

## Acceptance criteria

- [ ] 100% mutating routes have permission check
- [ ] Staff cannot delete restaurant (403 verified)
- [ ] Checklist committed to `backend/docs/route_permissions.md`
