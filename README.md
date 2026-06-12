# Architecture Teardown — Chef's Console (Sample)

This repository is a **complete Architecture Teardown deliverable** for [Chef's Console](https://chefsconsole.com), a multi-tenant restaurant bulk-order booking platform. It documents what exists today, what's fragile, and the exact sequence to fix it.

**Audience:** Non-technical founders (what to do next) and senior engineers / AI coding agents (how to execute).

## How to read this

| Folder | Part | Purpose |
|--------|------|---------|
| [00_AUDIT/](00_AUDIT/) | Part 1 | Forensic audit of the system you have today |
| [01_RESEARCH/](01_RESEARCH/) | Part 2 | Product definition — vision, users, flows |
| [02_BUILD_SPEC/](02_BUILD_SPEC/) | Part 3 | Executable blueprints — PRD, API, schema, RBAC |
| [03_WORK_BREAKDOWN/](03_WORK_BREAKDOWN/) | Part 4 | Epics → Features → Tasks, ready to assign |
| [04_AI_HARNESS/](04_AI_HARNESS/) | Part 5 | Agent loops, skills, guardrails for AI-assisted builds |
| [05_ROADMAP/](05_ROADMAP/) | Part 6 | Prioritized sequence — Now / Next / Later |

Start with [00_AUDIT/README.md](00_AUDIT/README.md) for the executive summary, then follow [05_ROADMAP/week_one_checklist.md](05_ROADMAP/week_one_checklist.md) to begin execution.

## Source system

- **Product:** Chef's Console — corporate bulk-order booking for restaurants
- **Stack:** FastAPI + MongoDB (backend), Next.js 15 (frontend + admin)
- **Repo:** This sample lives inside the audited codebase at `chefsconsole2/teardown-sample/`

## Anonymization

Product name and architecture are real. Client names, emails, credentials, and API keys are replaced with placeholders (`Acme Catering Ltd`, `client@example.com`, `[REDACTED]`).

## Live product

The final, corrected, and scale-ready MVP is live at [https://chefsconsole.com](https://chefsconsole.com).

---

*Architecture Teardown by V. Trivedy — vidhatatrivedy.com*
