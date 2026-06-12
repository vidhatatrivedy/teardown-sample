# EPIC-01 — Auth & Onboarding

**Capability:** Users can register, authenticate, complete onboarding, and access the product.

## Features

| ID | Feature | Tasks |
|----|---------|-------|
| FEAT-01-01 | JWT authentication | TASK-01-01-01, TASK-01-01-02 |
| FEAT-01-02 | Google OAuth | TASK-01-02-01 |
| FEAT-01-03 | Onboarding wizard | TASK-01-03-01, TASK-01-03-02 |
| FEAT-01-04 | Password recovery | TASK-01-04-01 |

## Dependencies

- None (foundation epic)

## Spec references

- [PRD § FR-1, FR-2](../../02_BUILD_SPEC/PRD.md)
- [system_design.md — Authentication](../../02_BUILD_SPEC/system_design.md)
- [api_reference.md — Auth](../../02_BUILD_SPEC/api_reference.md)

## Definition of done (epic)

- [ ] Signup → verify → login → onboarding → dashboard path works
- [ ] Token refresh on 401 in frontend
- [ ] Google OAuth alternate path works
- [ ] Password reset end-to-end
