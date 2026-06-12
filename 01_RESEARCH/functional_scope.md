# Functional Scope

## In scope

### Authentication & onboarding
- Email/password signup with verification
- Google OAuth sign-in
- Password reset flow
- Guided onboarding: create restaurant → activate subscription → connect email
- Profile management

### Restaurant & team
- Create and configure restaurant (settings, working hours, currency, timezone, bank details)
- Invite team members with roles (owner, manager, staff)
- Multi-restaurant membership (user can belong to multiple restaurants)

### Corporate clients
- CRUD for clients (company, contact, billing/delivery details, default pricing)
- Tour managers nested under clients
- Client/tour manager auto-match from AI extraction

### Enquiry pipeline
- List, filter, create, edit, reply to enquiries
- Status workflow: new → read → replied → approved/rejected → closed
- AI text extraction from pasted email content
- Bulk status update and delete
- Convert enquiry → booking + order (atomic business action)

### Bookings
- Editable table with inline updates
- Status, payment status, preparation status
- Bulk status and payment updates
- PDF invoice generation

### Orders
- CRUD linked to enquiry via `booking_reference`
- Calendar view of delivery schedule
- Line items with quantities and prices

### Email integration
- Connect Gmail or Outlook via OAuth (or IMAP)
- Background polling and processing
- Email inbox UI with thread view
- Create enquiry/booking from processed email

### Dashboard & analytics
- Summary stats: bookings, revenue, enquiries, clients
- Recent activity feeds

### Subscription administration
- Separate admin app to activate/deactivate restaurant subscriptions
- Frontend gate: dashboard blocked without active subscription

### Marketing & legal
- Landing, pricing, about, contact, privacy, terms pages

---

## Out of scope (explicit boundaries)

| Area | Reason |
|------|--------|
| Point of sale (POS) | Different product category |
| Inventory & recipe management | Not required for booking workflow |
| Consumer table reservations | B2B bulk orders only |
| Payment processing (Stripe etc.) | Payment *status* tracked; no card capture |
| Native mobile apps | Web responsive only |
| Multi-language UI | English only; timezone/currency configurable |
| Automated menu pricing engine | Manual `total_amount` and client default prices |
| CRM beyond clients/tour managers | No generic contact management |

## Scope creep watchlist

These often arrive as "small asks" but expand the build:

- WhatsApp/SMS enquiry intake
- Custom reporting / BI exports
- White-label per restaurant
- API for third-party integrations

Document any new request against this list before adding to the backlog.
