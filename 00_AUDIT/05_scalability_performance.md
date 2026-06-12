# Audit Dimension 05 — Scalability & Performance

**Severity:** High  
**Examined:** Bottlenecks, N+1 queries, caching, concurrency, background work

## Findings

### F5.1 — Email polling in API process (Critical at scale)

**Evidence:** `BackgroundTaskManager._monitor_integrations()` polls all active `EmailIntegration` records on an interval inside FastAPI.

**Risk:** CPU and connection pool contention with HTTP requests. Cannot scale API and workers independently.

**Direction:** Move to dedicated worker with per-integration job scheduling.

---

### F5.2 — Potential N+1 on list endpoints (High)

**Evidence:** `bookings.py` list handler enriches bookings with enquiry/client data per row (populate pattern in ~600-line router file).

**Risk:** 50 bookings → 50+ extra queries. Latency grows linearly with page size.

**Direction:** Batch-fetch related entities with `$in` queries or aggregation pipeline.

---

### F5.3 — No caching layer (Medium)

**Evidence:** Dashboard stats, taxonomy lists (timezones, currencies) hit DB/API every request.

**Risk:** Acceptable at low traffic. Taxonomy endpoints are good CDN/cache candidates.

**Direction:** Add HTTP cache headers on taxonomies; Redis for dashboard aggregates if needed.

---

### F5.4 — No rate limiting on API (Medium)

**Evidence:** No middleware for request throttling in `main.py`.

**Risk:** Auth endpoints and AI extraction endpoints vulnerable to abuse.

**Direction:** Add rate limits on `/auth/*` and `/extract-from-text`.

---

### F5.5 — Bulk operations exist (Positive)

**Evidence:** `POST /bookings/bulk/update-status`, bulk delete on enquiries — reduces round trips for ops users.

**Risk:** Large bulk payloads without size limits could timeout.

**Direction:** Cap batch size (e.g. 100 IDs) with clear error response.

---

### F5.6 — Single MongoDB connection pool (Acceptable)

**Evidence:** Motor async client in `database.py`.

**Risk:** Default pool settings may need tuning under concurrent email + API load.

**Direction:** Monitor connection count; configure `maxPoolSize` for production.

## Load breakpoints (estimated)

| Load | Likely failure |
|------|----------------|
| 10 restaurants, 100 bookings/day | None |
| 100 restaurants, active email polling | API latency spikes during poll cycles |
| 500+ bookings/restaurant, unindexed lists | Query timeouts on dashboard/bookings page |

**Business risk:** First real growth wave (multiple restaurants with live email integration) will expose in-process polling and N+1 list queries.
