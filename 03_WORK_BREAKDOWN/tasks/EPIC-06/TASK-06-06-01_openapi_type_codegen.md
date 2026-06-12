# TASK-06-06-01 — OpenAPI TypeScript type generation

**Epic:** EPIC-06  
**Feature:** FEAT-06-06 OpenAPI type codegen  
**Size:** M  
**Priority:** Medium

## Dependencies

TASK-06-02-01 (stable API surface)

## Context

Manual `types/index.ts` sync — Audit 04 F4.2.

## Work

1. Add script: fetch `/openapi.json` → `openapi-typescript` → `frontend/src/types/api.generated.ts`
2. Gradually replace hand-written types for core entities
3. Run codegen in CI on API change

## Acceptance criteria

- [ ] `npm run generate-types` produces TypeScript from live OpenAPI
- [ ] Enquiry, Booking, User types imported from generated file in api.ts
- [ ] CI fails if generated types out of date
