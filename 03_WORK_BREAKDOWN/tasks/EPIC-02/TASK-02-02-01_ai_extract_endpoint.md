# TASK-02-02-01 — AI extract-from-text with typed response

**Epic:** EPIC-02  
**Feature:** FEAT-02-02 AI text extraction  
**Size:** M  
**Priority:** High

## Dependencies

TASK-02-01-01

## Context

`POST .../enquiries/extract-from-text` uses `AIExtractionService`. Target typed `ExtractedEnquiryEntities` per [data_models_and_types.md](../../../02_BUILD_SPEC/data_models_and_types.md).

## Work

1. Add Pydantic response model for extraction
2. Cap input length at 15,000 chars → 413 if exceeded
3. Frontend modal shows field preview before save

## Acceptance criteria

- [ ] Paste sample email → fields populate in under 10s
- [ ] OpenAI failure falls back to DeepSeek with logged provider
- [ ] Empty extraction returns `extraction_status: failed` with message
