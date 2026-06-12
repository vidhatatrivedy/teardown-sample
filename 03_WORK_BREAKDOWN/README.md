# Part 4 — Work Breakdown

Epic → Feature → Task decomposition for Chef's Console. Every task is sized, sequenced, and includes acceptance criteria for cold pickup by an engineer or AI agent.

## Structure

```
epics/           Business capabilities
tasks/EPIC-XX/   Features (FEAT) and atomic tasks (TASK)
import/          GitHub issue export
```

## Conventions

| Prefix | Meaning |
|--------|---------|
| EPIC-XX | Business capability |
| FEAT-XX-YY | Shippable slice within epic |
| TASK-XX-YY-ZZ | One sitting of work |

**Size:** S (< 2h), M (2–4h), L (4–8h)

## Epic index

| Epic | Name | File |
|------|------|------|
| 01 | Auth & onboarding | [EPIC-01_auth_onboarding.md](epics/EPIC-01_auth_onboarding.md) |
| 02 | Enquiry pipeline | [EPIC-02_enquiry_pipeline.md](epics/EPIC-02_enquiry_pipeline.md) |
| 03 | Booking & order management | [EPIC-03_booking_order_management.md](epics/EPIC-03_booking_order_management.md) |
| 04 | Email integration & AI | [EPIC-04_email_integration_ai.md](epics/EPIC-04_email_integration_ai.md) |
| 05 | Team & RBAC | [EPIC-05_team_rbac.md](epics/EPIC-05_team_rbac.md) |
| 06 | Platform hardening | [EPIC-06_platform_hardening.md](epics/EPIC-06_platform_hardening.md) |

## Execution order (high level)

1. EPIC-06 critical security tasks first (tenant isolation, DEBUG fix)
2. EPIC-01 auth stable
3. EPIC-05 RBAC enforcement
4. EPIC-02 → EPIC-03 core pipeline
5. EPIC-04 email/AI
6. EPIC-06 remaining (tests, workers, consolidation)

See [05_ROADMAP/triage_now_next_later.md](../05_ROADMAP/triage_now_next_later.md).

## Import to GitHub

Use [import/github_issues.yaml](import/github_issues.yaml) with:

```bash
# Example: create issues from YAML (manual or script)
gh issue create --title "..." --body-file tasks/EPIC-06/TASK-06-01-01_....md
```
