# EPIC-03 — Booking & Order Management

**Capability:** Track confirmed bookings, payments, preparation, deliveries, and invoices.

## Features

| ID | Feature | Tasks |
|----|---------|-------|
| FEAT-03-01 | Booking table & CRUD | TASK-03-01-01 |
| FEAT-03-02 | Bulk booking updates | TASK-03-02-01 |
| FEAT-03-03 | Invoice generation | TASK-03-03-01 |
| FEAT-03-04 | Orders calendar | TASK-03-04-01 |

## Dependencies

- EPIC-02 (enquiries for conversion source)
- EPIC-01 (auth)

## Spec references

- [PRD § FR-6, FR-7](../../02_BUILD_SPEC/PRD.md)
- [frontend_specification.md — bookings, calendar](../../02_BUILD_SPEC/frontend_specification.md)

## Definition of done (epic)

- [ ] Bookings list with enquiry/client populate performs under 500ms p95 at 100 rows
- [ ] Bulk payment status update
- [ ] Invoice PDF downloads
- [ ] Calendar shows delivery events
