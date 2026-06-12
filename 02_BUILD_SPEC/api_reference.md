# API Reference

Base URL: `http://localhost:8000` (dev)  
Auth: `Authorization: Bearer <access_token>` unless noted  
OpenAPI: `/docs` and `/openapi.json` when server running

## Router index

| Prefix | Module | Auth |
|--------|--------|------|
| `/auth` | auth.py | Mixed |
| `/auth/google` | google_auth.py | Public |
| `/onboarding` | onboarding.py | JWT |
| `/restaurants` | restaurants.py, restaurants_enhanced.py | JWT |
| `/invitations` | invitations.py | JWT |
| `/restaurants/{id}/clients` | clients.py | JWT + RBAC |
| `/restaurants/{id}/tourmanagers` | tourmanagers.py | JWT + RBAC |
| `/restaurants/{id}/bookings` | bookings.py | JWT + RBAC |
| `/restaurants/{id}/orders` | orders.py | JWT + RBAC |
| `/restaurants/{id}/enquiries` | enquiries.py | JWT + RBAC |
| `/enquiries` | enquiries_standalone.py | JWT (**deprecate**) |
| `/restaurants/{id}/dashboard` | dashboard.py | JWT + RBAC |
| `/restaurants/{id}/email` | email_integration.py | JWT + RBAC |
| `/restaurants/{id}/email-processing` | email_processing.py | JWT + RBAC |
| `/taxonomies` | taxonomies.py | Public |
| `/admin` | admin.py | Admin token |

---

## Auth (`/auth`)

| Method | Path | Body | Response |
|--------|------|------|----------|
| POST | `/auth/signup` | `{email, password, full_name}` | `{access_token, refresh_token, user}` |
| POST | `/auth/login` | `{email, password}` | `{access_token, refresh_token, user}` |
| GET | `/auth/me` | — | `UserResponse` |
| POST | `/auth/refresh` | `{refresh_token}` | `{access_token, refresh_token}` |
| POST | `/auth/logout` | — | `{message}` |
| PUT | `/auth/profile` | `UserUpdate` | `UserResponse` |
| POST | `/auth/forgot-password` | `{email}` | `{message}` |
| POST | `/auth/reset-password` | `{token, new_password}` | `{message}` |
| POST | `/auth/verify-email` | `{token}` | `{message}` |

**Errors:** 401 invalid credentials; 400 email already registered

---

## Enquiries (`/restaurants/{restaurant_id}/enquiries`)

| Method | Path | Notes |
|--------|------|-------|
| GET | `/` | List; query: status, search |
| POST | `/` | Create `EnquiryCreate` |
| GET | `/{enquiry_id}` | Detail |
| PUT | `/{enquiry_id}` | Update |
| DELETE | `/{enquiry_id}` | Delete |
| PATCH | `/{enquiry_id}/status` | `{status}` |
| POST | `/{enquiry_id}/reply` | `EnquiryReply` |
| PATCH | `/{enquiry_id}/approve` | Sets approved |
| PATCH | `/{enquiry_id}/reject` | Sets rejected |
| POST | `/extract-from-text` | `{text}` → extracted fields |
| POST | `/{enquiry_id}/convert` | Creates Booking + Order |
| POST | `/bulk/update-status` | `{enquiry_ids, status}` |
| DELETE | `/bulk/delete` | `{enquiry_ids}` |
| GET | `/stats/summary` | Counts by status |

**EnquiryCreate shape:**
```json
{
  "booking_reference": "REF-001",
  "customer_name": "Jane Doe",
  "customer_email": "client@example.com",
  "customer_phone": "+1-555-0100",
  "subject": "Group lunch 50 pax",
  "message": "...",
  "client_id": "<ObjectId>",
  "tourmanager_id": null,
  "delivery_date": "2026-06-15",
  "delivery_time": "12:00",
  "tags": ["corporate"]
}
```

---

## Bookings (`/restaurants/{restaurant_id}/bookings`)

| Method | Path | Notes |
|--------|------|-------|
| GET | `/` | List with enquiry/client populate |
| POST | `/` | Create |
| GET | `/{booking_id}` | Detail |
| PUT | `/{booking_id}` | Update |
| DELETE | `/{booking_id}` | Delete |
| PATCH | `/{booking_id}/status` | Booking status |
| PATCH | `/{booking_id}/payment-status` | Payment status |
| PATCH | `/{booking_id}/preparation-status` | Kitchen prep |
| POST | `/bulk/update-status` | Bulk booking status |
| POST | `/bulk/update-payment-status` | Bulk payment |
| DELETE | `/bulk/delete` | Bulk delete |
| GET | `/stats/summary` | Aggregates |
| GET | `/{booking_id}/invoice` | PDF/HTML invoice |

---

## Orders (`/restaurants/{restaurant_id}/orders`)

| Method | Path | Notes |
|--------|------|-------|
| GET | `/` | List |
| POST | `/` | Create |
| GET | `/calendar/events` | FullCalendar format |
| GET | `/stats/summary` | Aggregates |
| GET | `/{order_id}` | Detail |
| PUT | `/{order_id}` | Update |
| DELETE | `/{order_id}` | Delete |

---

## Clients (`/restaurants/{restaurant_id}/clients`)

| Method | Path | Notes |
|--------|------|-------|
| GET | `/` | List active clients |
| POST | `/` | Create |
| GET | `/{client_id}` | Detail |
| PUT | `/{client_id}` | Update |
| DELETE | `/{client_id}` | Soft deactivate |
| POST | `/match-or-suggest` | AI client matching |
| GET | `/{client_id}/summary` | Stats |

---

## Email integration (`/restaurants/{restaurant_id}/email`)

| Method | Path | Notes |
|--------|------|-------|
| GET | `/integrations` | List connections |
| POST | `/integrations` | Create IMAP/OAuth |
| DELETE | `/integrations/{id}` | Remove |
| GET | `/oauth/gmail/authorize` | Redirect URL |
| GET | `/oauth/gmail/callback` | OAuth callback |

---

## Admin (`/admin`)

| Method | Path | Auth | Notes |
|--------|------|------|-------|
| POST | `/admin/login` | Public | `{username, password}` |
| GET | `/admin/restaurants` | Admin JWT | List all |
| PUT | `/admin/restaurants/{id}/subscription` | Admin JWT | Toggle active |

---

## Standard error responses

```json
{ "detail": "Human-readable message" }
```

```json
{
  "detail": [
    { "loc": ["body", "email"], "msg": "field required", "type": "value_error" }
  ]
}
```

## Pagination

Most list endpoints return full arrays today — **no cursor pagination**. Add `skip`/`limit` query params as hardening task (see EPIC-06).
