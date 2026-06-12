# User Behaviour

Observed and intended behaviour patterns for Chef's Console users.

## Email-first intake

**Pattern:** 60–80% of enquiries originate as inbound emails, not manual form entry.

**Behaviour:**
- James checks email inbox module morning and afternoon
- Low-confidence AI extractions are reviewed before saving
- Spam is ignored or deleted — not converted to enquiry
- Reply to customer happens in-product (`POST .../reply`) or back in Gmail depending on habit

**Product expectation:** Email processing must not auto-create bookings without explicit staff action.

---

## Paste-and-extract shortcut

**Pattern:** When email is already open in Gmail, James copies thread text into "Extract from text" rather than waiting for background sync.

**Behaviour:**
- Paste → review AI fields → adjust client match → save enquiry
- Client/tour manager match suggestions accepted ~50% of time; rest manual pick

**Product expectation:** Extraction under 5 seconds; clear indication when AI failed.

---

## Batch ops on booking day

**Pattern:** Day before delivery, James bulk-updates payment status and preparation status for 10–30 bookings.

**Behaviour:**
- Filter bookings by date
- Select rows → bulk update status
- Generate invoices individually for clients requiring PDF

**Product expectation:** Bulk actions must not timeout; progress feedback on large batches.

---

## Reluctance to delete

**Pattern:** Staff rarely delete enquiries or bookings — prefer status `closed` or `cancelled`.

**Behaviour:**
- Delete permission mainly used by managers cleaning test data
- Audit trail more important than storage cost at current scale

**Product expectation:** Soft-delete or status-based archive may be preferable long-term (out of current scope).

---

## Multi-restaurant switching

**Pattern:** Priya owns two restaurant locations; switches via restaurant selector in dashboard header.

**Behaviour:**
- Expects all lists to refresh to selected restaurant context
- Occasionally confused if backend uses stale `user.restaurant_id` (see Audit 07)

**Product expectation:** Switching restaurant must re-fetch all scoped data; no cross-tenant bleed.

---

## Subscription gate frustration

**Pattern:** New signup hits marketing pages freely; dashboard blocked until admin activates subscription.

**Behaviour:**
- Owner completes onboarding → lands on subscription-activation page → contacts support
- Admin activates in admin panel → owner refreshes → dashboard unlocks

**Product expectation:** Clear messaging on activation page with support contact (not a dead end).

---

## What users skip

- Restaurant working hours configuration (defaults accepted)
- Tour manager entity (skipped unless corporate client requires it)
- Order line-item detail (often single lump-sum line)
- Analytics beyond dashboard summary cards

Build priority should follow what users **do**, not every configured field.
