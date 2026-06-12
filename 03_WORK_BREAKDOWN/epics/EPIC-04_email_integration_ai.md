# EPIC-04 — Email Integration & AI

**Capability:** Connect email accounts, process inbound messages, review in inbox.

## Features

| ID | Feature | Tasks |
|----|---------|-------|
| FEAT-04-01 | OAuth email connect | TASK-04-01-01 |
| FEAT-04-02 | Background email sync | TASK-04-02-01, TASK-04-02-02 |
| FEAT-04-03 | Email inbox UI | TASK-04-03-01 |
| FEAT-04-04 | AI guardrails | TASK-04-04-01 |

## Dependencies

- EPIC-01 (auth)
- EPIC-02 (create enquiry from thread)

## Spec references

- [PRD § FR-8](../../02_BUILD_SPEC/PRD.md)
- [Audit 08 — AI layer](../../00_AUDIT/08_ai_model_layer.md)

## Definition of done (epic)

- [ ] Gmail OAuth connect and sync
- [ ] Email worker runs outside API process (or documented interim)
- [ ] Inbox shows threads with create-enquiry action
- [ ] AI cost cap per restaurant per day
