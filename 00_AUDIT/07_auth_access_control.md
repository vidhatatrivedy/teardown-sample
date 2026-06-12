# Audit Dimension 07 — Auth & Access Control

**Severity:** Critical  
**Examined:** Identity, RBAC, multi-tenant isolation

## Findings

### F7.1 — JWT auth with refresh (Positive)

**Evidence:** `backend/app/routers/auth.py` — signup, login, refresh, verify-token. Frontend `unified-auth-context.tsx` handles 401 retry.

**Risk:** Low for auth mechanism itself. Token storage in localStorage (typical SPA pattern) is XSS-sensitive.

**Direction:** Document XSS prevention requirements; consider httpOnly cookie strategy long-term.

---

### F7.2 — RBAC with three roles (Positive)

**Evidence:** `UserRole`: owner, manager, staff. `ROLE_PERMISSIONS` map in `permissions.py` with 30+ granular permissions.

**Risk:** Low if enforced everywhere. Staff role correctly limited on member management.

**Direction:** Permission matrix documented in `02_BUILD_SPEC/rbac_access_control.md`.

---

### F7.3 — Restaurant-scoped routes (Positive pattern)

**Evidence:** Most resources under `/restaurants/{restaurant_id}/...` with `verify_restaurant_access()` and `require_permission()`.

**Risk:** Pattern is sound when applied consistently.

**Direction:** Extend to all resources; remove exceptions.

---

### F7.4 — Standalone enquiry router scoping (Critical)

**Evidence:** `enquiries_standalone.router` at prefix `/enquiries` uses `current_user.restaurant_id` from user document, not URL path. Overlaps with scoped router.

**Risk:** If `user.restaurant_id` is stale or wrong after multi-restaurant switch, operations may target wrong tenant. Two APIs for same resource increases audit surface.

**Direction:** Deprecate standalone router; frontend should only call scoped endpoints. Add integration tests for cross-tenant access attempts (expect 403).

---

### F7.5 — Multi-restaurant user model gap (High)

**Evidence:** User model has single `restaurant_id` field. `RestaurantProvider` on frontend supports selecting among user's restaurants via members list, but user document stores one `restaurant_id`.

**Risk:** Context switch may not update backend user record; standalone routes use potentially wrong tenant.

**Direction:** Remove `restaurant_id` from User; always pass `restaurant_id` in URL or header; validate membership on every request.

---

### F7.6 — Subscription gate (Medium)

**Evidence:** `is_subscription_active` on Restaurant; frontend `AuthWrapper` blocks dashboard without active subscription.

**Risk:** Backend must also enforce — API calls with valid JWT but inactive subscription should return 403 on mutating routes.

**Direction:** Add subscription middleware on restaurant-scoped write endpoints.

---

### F7.7 — Invitation token flow (Positive)

**Evidence:** `RestaurantInvitation` with expiring token, accept flow at `/invite/accept`.

**Risk:** Token in URL could leak via referrer logs if external links clicked carelessly.

**Direction:** Short expiry (present); POST accept with token in body preferred over GET.

## Tenant isolation test matrix (required)

| Action | Expected |
|--------|----------|
| User A requests User B's restaurant bookings | 403 |
| User A with valid JWT, wrong restaurant_id in URL | 403 |
| Staff role attempts DELETE restaurant | 403 |
| Expired subscription, POST booking | 403 |

**Business risk:** This is the highest diligence risk. Cross-tenant data exposure is existentially bad for a multi-tenant SaaS. Fix before scaling customers.
