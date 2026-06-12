# User Personas

## Persona 1 — Restaurant Owner (Priya)

**Role:** Owner of a mid-size restaurant with corporate catering revenue  
**Tech comfort:** Moderate — uses Gmail, spreadsheets, WhatsApp for business  
**Goals:** See pipeline health, control who on staff can change prices, ensure subscription is active  
**Frustrations:** Doesn't know if enquiries are being missed; can't audit staff actions  
**Uses:** Dashboard stats, restaurant settings, team invites, subscription activation  
**Permissions:** Owner — full access

---

## Persona 2 — Operations Manager (James)

**Role:** Runs day-to-day booking and delivery coordination  
**Tech comfort:** High — lives in the product daily  
**Goals:** Convert enquiries fast, batch-update booking statuses, generate invoices, view delivery calendar  
**Frustrations:** Re-typing email content; broken link between enquiry and kitchen order  
**Uses:** Enquiries, bookings table, orders calendar, email inbox, AI paste extraction  
**Permissions:** Manager — all ops, limited member management

---

## Persona 3 — Front-of-house Staff (Sam)

**Role:** Answers emails, creates enquiries, updates booking contact details  
**Tech comfort:** Low-moderate  
**Goals:** Log enquiries accurately, reply to customers, avoid breaking anything  
**Frustrations:** Too many fields; unclear when enquiry becomes a booking  
**Uses:** Enquiries list, manual create, reply flow  
**Permissions:** Staff — view/create enquiries and bookings; no delete restaurant, no member admin

---

## Persona 4 — Subscription Admin (Internal — Alex)

**Role:** Chef's Console operator managing paying restaurants  
**Tech comfort:** High  
**Goals:** Activate subscription after payment, deactivate churned accounts  
**Uses:** Admin panel at port 3002 — login, restaurant list, subscription toggle  
**Permissions:** Separate admin auth (not restaurant RBAC)

---

## Persona 5 — Corporate Client Contact (External — not a user)

**Role:** Tour operator or company event planner sending enquiry emails  
**Does not log in** — interacts via email only  
**Expects:** Timely reply, clear booking reference, invoice with correct company name  

Their behaviour is captured in [user_behaviour.md](user_behaviour.md) as inbound email patterns, not product usage.

## Persona priority for build

**Primary:** Operations Manager (James) — optimize enquiry→booking flow  
**Secondary:** Restaurant Owner (Priya) — dashboard and team control  
**Tertiary:** Staff (Sam) — simplify create/reply UX
