# Part 3 — Build Specification

Executable blueprints for Chef's Console. Hand this folder to an engineer or AI agent — every document is written to be built from.

## Reading order

1. [PRD.md](PRD.md) — source of truth for *what* and *why*
2. [technical_architecture.md](technical_architecture.md) — stack and tradeoffs
3. [system_design.md](system_design.md) — components and sequences
4. [database_schema.md](database_schema.md) — ER diagram and indexes
5. [data_models_and_types.md](data_models_and_types.md) — canonical types
6. [api_reference.md](api_reference.md) — endpoint contracts
7. [rbac_access_control.md](rbac_access_control.md) — roles and tenant rules
8. [frontend_specification.md](frontend_specification.md) — screens and states
9. [design_system.md](design_system.md) — UI tokens and patterns
10. [security_model.md](security_model.md) — threats and controls

## Principle

**Diagram first.** If it can be an ER diagram, sequence diagram, or component diagram, it should be — not three paragraphs of prose.

## Traceability

| Research | Build spec |
|----------|------------|
| [01_RESEARCH/vision_and_why.md](../01_RESEARCH/vision_and_why.md) | PRD §1 |
| [01_RESEARCH/functional_scope.md](../01_RESEARCH/functional_scope.md) | PRD §2 |
| [01_RESEARCH/user_flows.md](../01_RESEARCH/user_flows.md) | system_design.md, frontend_specification.md |

## Source code reference

Implementation lives in the parent repo:

- Backend: `backend/app/`
- Frontend: `frontend/src/`
- Admin: `admin/src/`
