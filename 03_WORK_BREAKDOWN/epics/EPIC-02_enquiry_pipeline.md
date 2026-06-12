# EPIC-02 — Enquiry Pipeline

**Capability:** Staff intake, manage, and convert customer enquiries.

## Features

| ID | Feature | Tasks |
|----|---------|-------|
| FEAT-02-01 | Enquiry CRUD | TASK-02-01-01 |
| FEAT-02-02 | AI text extraction | TASK-02-02-01, TASK-02-02-02 |
| FEAT-02-03 | Enquiry conversion | TASK-02-03-01 |
| FEAT-02-04 | Bulk enquiry ops | TASK-02-04-01 |

## Dependencies

- EPIC-01 (auth)
- EPIC-05 (client permissions)
- Clients must exist (EPIC-05 / client CRUD)

## Spec references

- [PRD § FR-5](../../02_BUILD_SPEC/PRD.md)
- [data_models_and_types.md — Enquiry](../../02_BUILD_SPEC/data_models_and_types.md)
- [user_flows.md — Flow 2](../../01_RESEARCH/user_flows.md)

## Definition of done (epic)

- [ ] Full enquiry status workflow
- [ ] AI extract populates form with error handling
- [ ] Convert creates booking + order atomically
- [ ] Bulk status update for 50+ enquiries
