# EPIC-06 — Platform Hardening

**Capability:** Production readiness — security, tests, performance, consolidation.

## Features

| ID | Feature | Tasks |
|----|---------|-------|
| FEAT-06-01 | Tenant isolation fix | TASK-06-01-01, TASK-06-01-02 |
| FEAT-06-02 | Router consolidation | TASK-06-02-01 |
| FEAT-06-03 | Test suite & CI | TASK-06-03-01, TASK-06-03-02 |
| FEAT-06-04 | Database indexes & migrations | TASK-06-04-01 |
| FEAT-06-05 | Security hardening | TASK-06-05-01 |
| FEAT-06-06 | OpenAPI type codegen | TASK-06-06-01 |

## Dependencies

- Audit complete (00_AUDIT)
- Should run **in parallel with or before** scaling customers

## Spec references

- [00_AUDIT/README.md](../../00_AUDIT/README.md) — all findings
- [05_ROADMAP/triage_now_next_later.md](../../05_ROADMAP/triage_now_next_later.md)

## Definition of done (epic)

- [ ] No standalone `/enquiries` router in production
- [ ] pytest CI green on PR
- [ ] DEBUG handler safe in production
- [ ] Compound indexes on bookings/enquiries/orders
- [ ] Frontend types generated from OpenAPI

## Priority

**Execute FEAT-06-01 and FEAT-06-05 first** — before new feature work.
