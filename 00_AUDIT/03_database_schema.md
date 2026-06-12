# Audit Dimension 03 — Database Design & Schema

**Severity:** Medium  
**Examined:** Collections, relationships, indexes, normalization, constraints

## Findings

### F3.1 — MongoDB via Beanie ODM (Documented choice)

**Evidence:** 14 document models registered in `backend/app/database.py`.

**Risk:** Flexible schema suits MVP iteration. Relational reporting (joins across tenants) is harder than SQL.

**Direction:** Accept for current scale; add aggregation pipelines for analytics if needed.

---

### F3.2 — String foreign keys instead of DB refs (Medium)

**Evidence:** `restaurant_id`, `client_id`, `enquiry_id`, `created_by` stored as strings across `Enquiry`, `Booking`, `Order`, `Client`.

**Risk:** No database-enforced referential integrity. Orphan records possible if deletes aren't cascaded in application code.

**Direction:** Add application-level cascade rules; consider Beanie `Link` types for critical relations.

---

### F3.3 — Sparse indexing strategy (Medium)

**Evidence:** Some models define indexes (`Client`: `restaurant_id`, `email`; `Restaurant`: `owner_id`). Others like `Booking`, `Enquiry`, `Order` have no explicit indexes in model `Settings`.

**Risk:** List/filter queries by `restaurant_id` + date will full-scan as data grows.

**Direction:** Add compound indexes: `{restaurant_id: 1, created_at: -1}` on bookings, enquiries, orders.

---

### F3.4 — No migration framework (High)

**Evidence:** Schema changes applied by editing Beanie models directly. No Alembic/Flyway equivalent for MongoDB.

**Risk:** Production data may not match new model fields. Rolling deploys can break reads.

**Direction:** Introduce versioned migration scripts (e.g. `migrate-mongo`, custom scripts in `backend/migrations/`).

---

### F3.5 — Shared booking_reference across entities (Positive)

**Evidence:** `booking_reference` on Enquiry, Booking, Order enables traceability without joins.

**Risk:** Low if uniqueness enforced per restaurant. Currently no unique index on `(restaurant_id, booking_reference)`.

**Direction:** Add unique compound index to prevent duplicate references.

---

### F3.6 — Embedded vs referenced data (Acceptable)

**Evidence:** `Restaurant.members` embedded as list; `RestaurantSettings`, `BankDetails` nested Pydantic models. Clients/Bookings are separate collections.

**Risk:** Large member lists could hit document size limits (unlikely at MVP scale).

**Direction:** Monitor; extract members to collection if teams exceed ~50 per restaurant.

## Collections inventory

| Collection | Tenant key | Notable fields |
|------------|------------|----------------|
| users | — | email, restaurant_id, onboarding flags |
| restaurants | owner_id | members[], settings, subscription |
| clients | restaurant_id | company_name, pricing defaults |
| tourmanagers | restaurant_id | client_id |
| enquiries | restaurant_id | client_id, extracted_entities |
| bookings | restaurant_id | enquiry_id, booking_reference |
| orders | restaurant_id | enquiry_id, items[] |
| email_integrations | restaurant_id | OAuth tokens |
| email_threads / email_messages | restaurant_id | processing metadata |
| restaurant_invitations | restaurant_id | token, status |
| password_reset_tokens | — | token, expiry |
| email_verification_tokens | — | token, expiry |

## Summary

**Business risk:** Migration pain and slow queries will surface at ~1000 bookings/restaurant without indexes and migration discipline.
