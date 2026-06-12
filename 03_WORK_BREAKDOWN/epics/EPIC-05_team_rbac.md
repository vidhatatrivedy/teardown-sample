# EPIC-05 — Team & RBAC

**Capability:** Multi-user restaurants with role-based access and invitations.

## Features

| ID | Feature | Tasks |
|----|---------|-------|
| FEAT-05-01 | Role permission enforcement | TASK-05-01-01 |
| FEAT-05-02 | Team invitations | TASK-05-02-01 |
| FEAT-05-03 | Client & tour manager CRUD | TASK-05-03-01 |
| FEAT-05-04 | Subscription gate (backend) | TASK-05-04-01 |

## Dependencies

- EPIC-01 (auth)

## Spec references

- [rbac_access_control.md](../../02_BUILD_SPEC/rbac_access_control.md)
- [Audit 07](../../00_AUDIT/07_auth_access_control.md)

## Definition of done (epic)

- [ ] All mutating routes call `require_permission`
- [ ] Cross-tenant access tests pass
- [ ] Invite → accept → dashboard with correct role
- [ ] Inactive subscription returns 403 on writes
