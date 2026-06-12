# Week One Checklist

Unambiguous first-week actions. Works for Track A (founder+AI) and Track B (engineering).

## Before writing code

- [ ] Read [00_AUDIT/README.md](../00_AUDIT/README.md) — 10 min
- [ ] Read [triage_now_next_later.md](triage_now_next_later.md) — 5 min
- [ ] Copy AI harness rules to `.cursor/rules/` (Track A)
- [ ] Confirm local stack runs: backend :8000, frontend :3000, MongoDB connected
- [ ] Confirm `.env` not committed; credentials are `[REDACTED]` in docs

## Day 1 — Tenant surface reduction

- [ ] Execute [TASK-06-01-01](../03_WORK_BREAKDOWN/tasks/EPIC-06/TASK-06-01-01_remove_standalone_enquiries_router.md)
- [ ] Grep codebase: no frontend calls to unscoped `/enquiries`
- [ ] Manual test: create enquiry from dashboard still works
- [ ] Run [review_loop.md](../04_AI_HARNESS/agent_loops/review_loop.md)

## Day 2 — Security quick wins

- [ ] Execute [TASK-06-05-01](../03_WORK_BREAKDOWN/tasks/EPIC-06/TASK-06-05-01_debug_handler_oauth_encryption.md)
- [ ] Verify forced 500 returns generic message only
- [ ] If email integrated locally, verify sync still works after token encryption

## Day 3 — Prove isolation

- [ ] Execute [TASK-06-01-02](../03_WORK_BREAKDOWN/tasks/EPIC-06/TASK-06-01-02_cross_tenant_integration_tests.md)
- [ ] **Human review required:** read test assertions — do they actually attempt cross-tenant access?
- [ ] All isolation tests pass

## Day 4 — Permission audit start

- [ ] Execute [TASK-05-01-01](../03_WORK_BREAKDOWN/tasks/EPIC-05/TASK-05-01-01_audit_require_permission.md) (may spill to Day 5)
- [ ] Produce route → permission checklist

## Day 5 — Subscription + smoke test

- [ ] Execute [TASK-05-04-01](../03_WORK_BREAKDOWN/tasks/EPIC-05/TASK-05-04-01_subscription_middleware.md)
- [ ] Full smoke test path:
  1. Login as staff@example.com (test account)
  2. Select restaurant
  3. Create client "Acme Catering Ltd"
  4. Create enquiry linked to client
  5. Convert to booking
  6. View booking on calendar
- [ ] Deactivate subscription in admin → confirm write blocked

## End of week 1 — Go / no-go

| Check | Pass? |
|-------|-------|
| No standalone `/enquiries` router | |
| Cross-tenant tests pass | |
| DEBUG handler safe | |
| Subscription enforced on backend writes | |
| Smoke test complete | |

**Go:** Proceed to Week 2 (pytest + CI) per [track_b_engineering_team.md](track_b_engineering_team.md) or Week 2 tasks in [track_a_founder_ai.md](track_a_founder_ai.md).

**No-go:** Do not onboard new paying customers until Critical **Now** items pass.

## Support references

- Stuck on task → re-read linked spec in `02_BUILD_SPEC/`
- Agent going off-rails → [project-guardrails.mdc](../04_AI_HARNESS/.cursor/rules/project-guardrails.mdc)
- Priority dispute → [triage_now_next_later.md](triage_now_next_later.md) wins
