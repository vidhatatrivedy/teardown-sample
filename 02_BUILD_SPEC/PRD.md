# Product Requirements Document (PRD)

**Product:** Chef's Console  
**Version:** 1.0 (MVP + hardening target)  
**Status:** Approved for rebuild/refactor execution

---

## 1. Problem & vision

See [01_RESEARCH/vision_and_why.md](../01_RESEARCH/vision_and_why.md).

**Summary:** Restaurants managing corporate bulk orders need one system to intake enquiries (especially email), confirm bookings, coordinate delivery orders, and invoice clients — with team access control.

---

## 2. Functional requirements

### FR-1 Authentication
- FR-1.1 Email/password registration with email verification
- FR-1.2 Login with JWT access + refresh tokens
- FR-1.3 Google OAuth alternative login
- FR-1.4 Password reset via email token
- FR-1.5 Profile view and update

### FR-2 Onboarding
- FR-2.1 Multi-step onboarding wizard after signup
- FR-2.2 Create first restaurant during onboarding
- FR-2.3 Block dashboard until subscription active (with clear UX)
- FR-2.4 Optional email integration step

### FR-3 Multi-tenant restaurant
- FR-3.1 User may belong to multiple restaurants via membership
- FR-3.2 All business data scoped by `restaurant_id`
- FR-3.3 Restaurant settings: currency, timezone, working hours, bank details
- FR-3.4 Team invites with role assignment

### FR-4 Clients & tour managers
- FR-4.1 CRUD clients per restaurant
- FR-4.2 CRUD tour managers linked to client
- FR-4.3 AI-assisted client/tour manager match from extracted text

### FR-5 Enquiries
- FR-5.1 CRUD enquiries with status workflow
- FR-5.2 Reply to enquiry (stores reply message + timestamp)
- FR-5.3 AI extract fields from pasted text
- FR-5.4 Bulk status update and delete
- FR-5.5 Convert approved enquiry to booking + order

### FR-6 Bookings
- FR-6.1 CRUD bookings linked to enquiry
- FR-6.2 Track booking, payment, preparation status
- FR-6.3 Bulk status and payment updates
- FR-6.4 Generate invoice PDF

### FR-7 Orders
- FR-7.1 CRUD orders with line items
- FR-7.2 Calendar view of deliveries
- FR-7.3 Shared `booking_reference` with enquiry and booking

### FR-8 Email
- FR-8.1 OAuth connect Gmail/Outlook
- FR-8.2 Background sync and AI processing
- FR-8.3 Inbox UI with thread detail
- FR-8.4 Manual create enquiry from email thread

### FR-9 Dashboard
- FR-9.1 Aggregate stats per restaurant
- FR-9.2 Recent activity lists

### FR-10 Admin
- FR-10.1 Separate admin login
- FR-10.2 List restaurants and toggle subscription

---

## 3. Non-functional requirements

| ID | Requirement |
|----|-------------|
| NFR-1 | API p95 latency under 500ms for list endpoints at 100 records |
| NFR-2 | Tenant isolation — zero cross-restaurant data access |
| NFR-3 | RBAC enforced on all mutating endpoints |
| NFR-4 | Secrets never in client bundle or git |
| NFR-5 | AI extraction failures degrade gracefully with user message |
| NFR-6 | Responsive web UI — desktop primary, tablet acceptable |

---

## 4. Out of scope

See [01_RESEARCH/functional_scope.md](../01_RESEARCH/functional_scope.md) § Out of scope.

---

## 5. Success criteria

- [ ] Ops manager completes enquiry→booking in under 5 minutes
- [ ] Cross-tenant access tests pass (403 on all unauthorized attempts)
- [ ] pytest suite covers auth, enquiry convert, RBAC
- [ ] OpenAPI-generated types used on frontend
- [ ] Email worker runs outside API process

---

## 6. Open decisions (resolved for build)

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Database | MongoDB + Beanie | Already in production; migration cost too high |
| Auth transport | JWT Bearer header | Existing implementation |
| AI providers | OpenAI primary, DeepSeek fallback | Cost/resilience balance |
| Payment | Status tracking only | No Stripe in MVP scope |
