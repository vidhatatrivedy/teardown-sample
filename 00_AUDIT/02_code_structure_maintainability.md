# Audit Dimension 02 — Code Structure & Maintainability

**Severity:** Medium  
**Examined:** Module boundaries, duplication, dead code, readability

## Findings

### F2.1 — Oversized frontend API client (High)

**Evidence:** `frontend/src/lib/api.ts` — ~1100 lines, single `ApiClient` class with all HTTP methods.

**Risk:** Every API change touches a monolith file. Merge conflicts and missed endpoints increase with team size.

**Direction:** Split by domain module (`bookingsApi`, `enquiriesApi`, etc.) or generate from OpenAPI spec.

---

### F2.2 — Oversized shared types file (Medium)

**Evidence:** `frontend/src/types/index.ts` — ~1000 lines, all interfaces in one export.

**Risk:** Hard to navigate; no enforced link to backend Pydantic models.

**Direction:** Split by domain; consider codegen from backend OpenAPI.

---

### F2.3 — Ad-hoc test scripts, no pytest suite (High)

**Evidence:** Root and `backend/` contain scripts like `test_api.py`, `test_email_processing.py`, `integration_test.py` — not organized under `tests/` with CI.

**Risk:** No regression gate on deploy. Engineers run tests manually or skip them.

**Direction:** Migrate critical paths to `pytest` + GitHub Actions; keep integration tests behind env flag.

---

### F2.4 — Stale frontend README (Low)

**Evidence:** `frontend/README.md` states "Backend Coming Soon" while backend is fully implemented.

**Risk:** Onboarding friction for new contributors.

**Direction:** Update README or remove misleading sections.

---

### F2.5 — Consistent component organization (Positive)

**Evidence:** Domain folders under `frontend/src/components/` (`bookings/`, `enquiries/`, `clients/`, `email-inbox/`).

**Risk:** Low. Feature-based grouping aids navigation.

**Direction:** Maintain convention; document in frontend spec.

---

### F2.6 — Permission logic centralized (Positive)

**Evidence:** `backend/app/utils/permissions.py` — single `ROLE_PERMISSIONS` map and `require_permission()` helper.

**Risk:** Low if all routes use it consistently. Standalone routers need verification (see Audit 07).

**Direction:** Lint or test that every mutating route calls permission check.

## Summary

| Finding | Severity |
|---------|----------|
| F2.1 Monolithic api.ts | High |
| F2.3 No formal test suite | High |
| F2.2 Monolithic types | Medium |
| F2.4 Stale README | Low |
| F2.5 Component folders | Low (positive) |
| F2.6 Centralized permissions | Low (positive) |

**Business risk:** Release velocity slows as files grow. Without CI tests, each release is a manual bet.
