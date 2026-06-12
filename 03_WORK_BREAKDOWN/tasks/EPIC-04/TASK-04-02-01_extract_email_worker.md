# TASK-04-02-01 — Extract email worker from API process

**Epic:** EPIC-04  
**Feature:** FEAT-04-02 Background email sync  
**Size:** L  
**Priority:** High

## Dependencies

TASK-04-01-01

## Context

`BackgroundTaskManager` runs inside FastAPI lifespan — Audit 05 Critical at scale.

## Work

1. Create `backend/worker.py` entry point running same poll loop
2. Remove `start_background_tasks()` from API lifespan (or gate with env `RUN_WORKER=false`)
3. Document deploy: API + worker as separate processes

## Acceptance criteria

- [ ] API restart does not run email poll when worker disabled
- [ ] Worker process polls all active integrations
- [ ] Stuck job cleanup still runs on worker start
