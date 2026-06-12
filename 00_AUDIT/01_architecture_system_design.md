# Audit Dimension 01 — Architecture & System Design

**Severity:** High  
**Examined:** Service boundaries, coupling, data flow, single points of failure

## Findings

### F1.1 — Monorepo with three deployable apps (Acceptable)

**Evidence:** `frontend/` (port 3000), `backend/` (port 8000), `admin/` (port 3002) share one repo but deploy independently.

**Risk:** Low for current stage. Deployment scripts (`backend/deploy.sh`) only cover the API; frontend/admin deploy paths are undocumented.

**Direction:** Document deploy topology in build spec; consider shared env conventions.

---

### F1.2 — Duplicate restaurant routers (High)

**Evidence:** `backend/app/main.py` mounts both `restaurants.router` ("backward compatibility") and `restaurants_enhanced.router`.

**Risk:** Two code paths for the same domain concept. Bug fixes may land on one router only. New engineers won't know which to extend.

**Direction:** Consolidate into a single router module; deprecate with migration notes.

---

### F1.3 — Duplicate enquiry routers (Critical)

**Evidence:** `enquiries.router` (scoped under `/restaurants/{restaurant_id}/enquiries`) and `enquiries_standalone.router` (prefix `/enquiries`) both registered in `main.py`.

**Risk:** Different authorization paths for the same entity. Standalone router uses `current_user.restaurant_id` from the user document rather than URL path — inconsistent with rest of API.

**Direction:** Merge into one router pattern; audit all standalone endpoints for tenant checks.

---

### F1.4 — In-process background task manager (High)

**Evidence:** `BackgroundTaskManager` in `backend/app/services/background_task_manager.py` runs asyncio tasks inside the FastAPI process lifespan.

**Risk:** Email polling for all integrations shares one process. Restart, OOM, or deploy kills all background work. No horizontal scaling path.

**Direction:** Extract to a dedicated worker (Celery, ARQ, or cloud queue) with health checks.

---

### F1.5 — Layered backend structure (Positive)

**Evidence:** Clear separation — `routers/` → `services/` → `models/` → `utils/`.

**Risk:** Low. Pattern is consistent and teachable.

**Direction:** Preserve; enforce via AI harness rules.

---

### F1.6 — Central enquiry→booking→order pipeline (Positive)

**Evidence:** `Enquiry`, `Booking`, `Order` linked by `booking_reference` and `enquiry_id`. Convert endpoint at `POST /restaurants/{id}/enquiries/{id}/convert`.

**Risk:** Low architecturally. Business logic for conversion is concentrated in one router — good for auditability.

**Direction:** Document sequence diagram in build spec (done in `02_BUILD_SPEC/system_design.md`).

## Summary

| Finding | Severity |
|---------|----------|
| F1.3 Duplicate enquiry routers | Critical |
| F1.2 Duplicate restaurant routers | High |
| F1.4 In-process background jobs | High |
| F1.1 Three-app monorepo | Medium |
| F1.5 Layered backend | Low (positive) |
| F1.6 Enquiry pipeline | Low (positive) |

**Business risk:** Architecture will not survive 10× tenant growth without worker extraction and router consolidation. Diligence reviewers will flag duplicate API surfaces.
