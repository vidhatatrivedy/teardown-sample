# Triage — Now / Next / Later

Ordered by **risk and dependency**, not by what looks worst on the surface.

---

## NOW — Fix before scaling customers or diligence

Production or diligence failures if skipped.

| Task | Audit | Effort | Why now |
|------|-------|--------|---------|
| [TASK-06-01-01](../03_WORK_BREAKDOWN/tasks/EPIC-06/TASK-06-01-01_remove_standalone_enquiries_router.md) | 07 F7.4 | M | Cross-tenant data risk |
| [TASK-06-05-01](../03_WORK_BREAKDOWN/tasks/EPIC-06/TASK-06-05-01_debug_handler_oauth_encryption.md) | 06 F6.1, F6.3 | M | Stack trace + token leak |
| [TASK-06-01-02](../03_WORK_BREAKDOWN/tasks/EPIC-06/TASK-06-01-02_cross_tenant_integration_tests.md) | 07 | L | Prove isolation |
| [TASK-05-01-01](../03_WORK_BREAKDOWN/tasks/EPIC-05/TASK-05-01-01_audit_require_permission.md) | 07 | L | RBAC gaps |
| [TASK-05-04-01](../03_WORK_BREAKDOWN/tasks/EPIC-05/TASK-05-04-01_subscription_middleware.md) | 07 F7.6 | M | Backend subscription bypass |

**Founder summary:** These five tasks stop the scenarios that kill a fundraise or leak customer data. Do them first even though users can't see the difference.

---

## NEXT — Unblocks scale once foundation holds

| Task | Audit | Effort | Why next |
|------|-------|--------|----------|
| [TASK-06-03-01](../03_WORK_BREAKDOWN/tasks/EPIC-06/TASK-06-03-01_pytest_structure.md) | 02 F2.3 | L | Regression safety |
| [TASK-06-03-02](../03_WORK_BREAKDOWN/tasks/EPIC-06/TASK-06-03-02_github_actions_ci.md) | 02 | M | Automated gate |
| [TASK-06-02-01](../03_WORK_BREAKDOWN/tasks/EPIC-06/TASK-06-02-01_consolidate_restaurant_routers.md) | 01 F1.2 | M | Maintainability |
| [TASK-04-02-01](../03_WORK_BREAKDOWN/tasks/EPIC-04/TASK-04-02-01_extract_email_worker.md) | 05 F5.1 | L | Scale email load |
| [TASK-03-01-01](../03_WORK_BREAKDOWN/tasks/EPIC-03/TASK-03-01-01_bookings_list_optimize.md) | 05 F5.2 | L | Performance |
| [TASK-06-04-01](../03_WORK_BREAKDOWN/tasks/EPIC-06/TASK-06-04-01_compound_indexes_migrations.md) | 03 F3.3 | M | Query speed |
| [TASK-02-03-01](../03_WORK_BREAKDOWN/tasks/EPIC-02/TASK-02-03-01_enquiry_convert_atomic.md) | — | L | Core pipeline reliability |
| [TASK-01-01-01](../03_WORK_BREAKDOWN/tasks/EPIC-01/TASK-01-01-01_jwt_login_refresh.md) | — | M | Auth stability |

---

## LATER — Safe to defer

| Task | Notes |
|------|-------|
| [TASK-06-06-01](../03_WORK_BREAKDOWN/tasks/EPIC-06/TASK-06-06-01_openapi_type_codegen.md) | High value, not blocking launch |
| [TASK-04-04-01](../03_WORK_BREAKDOWN/tasks/EPIC-04/TASK-04-04-01_ai_cost_cap.md) | Needed before heavy AI usage |
| [TASK-02-04-01](../03_WORK_BREAKDOWN/tasks/EPIC-02/TASK-02-04-01_bulk_enquiry_status.md) | Nice-to-have ops feature |
| [TASK-03-03-01](../03_WORK_BREAKDOWN/tasks/EPIC-03/TASK-03-03-01_invoice_pdf_generation.md) | Works today — polish pass |
| Design system expansion | After core hardening |
| Analytics depth | After dashboard perf |

---

## Deliberately leave alone (for now)

- Marketing page copy and styling
- FullCalendar theme tweaks
- MongoDB → PostgreSQL migration (not justified)
- Rewriting frontend in different framework

---

## Risk if "Later" becomes "Never"

| Deferred item | Consequence |
|---------------|-------------|
| AI cost cap | Surprise OpenAI bill |
| OpenAPI codegen | Type drift bugs in production |
| Email worker split | Outages when customer count grows |

Review this triage monthly — move items up if usage patterns change.
