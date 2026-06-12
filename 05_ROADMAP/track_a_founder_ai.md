# Track A — Founder + AI

For a non-technical founder driving the build with Cursor, Claude Code, or similar agents.

## Setup (Day 0)

1. Clone repo with `teardown-sample/` folder
2. Copy guardrails:
   ```bash
   cp teardown-sample/04_AI_HARNESS/.cursor/rules/*.mdc .cursor/rules/
   ```
3. Ensure backend venv and MongoDB running locally
4. Read [00_AUDIT/README.md](../00_AUDIT/README.md) executive summary (15 min)

## Weekly rhythm

| Day | Activity |
|-----|----------|
| Mon | Pick 2–3 tasks from **Now** bucket |
| Tue–Thu | Run agent on one task at a time using [task_executor.md](../04_AI_HARNESS/prompts/task_executor.md) |
| Fri | Manual smoke test: login → enquiry → convert → booking |
| Async | Paste agent output to technical advisor for review on Critical tasks |

## Task order (weeks 1–4)

### Week 1 — Stop the bleeding
1. TASK-06-01-01 Remove standalone enquiries router
2. TASK-06-05-01 DEBUG handler + OAuth encryption
3. TASK-06-01-02 Cross-tenant tests *(bring human reviewer)*

### Week 2 — Prove enforcement
4. TASK-05-01-01 Permission audit
5. TASK-05-04-01 Subscription middleware

### Week 3 — Safety net
6. TASK-06-03-01 pytest structure *(human helpful)*
7. TASK-06-03-02 GitHub Actions CI *(human helpful)*

### Week 4 — Core pipeline
8. TASK-02-03-01 Atomic enquiry convert
9. TASK-03-01-01 Bookings list optimization

## When to bring a human in

| Moment | Why |
|--------|-----|
| Before TASK-06-01-02 | Validate tests actually prove isolation |
| Before CI setup | GitHub secrets and Mongo service |
| Before production deploy | Env vars, SSL, backup |
| Any migration on live data | Irreversible if wrong |

Budget ~4–8 hours/week of senior engineer review during **Now** phase.

## Agent prompt template

```
Execute task: teardown-sample/03_WORK_BREAKDOWN/tasks/EPIC-06/TASK-06-01-01_remove_standalone_enquiries_router.md

Follow teardown-sample/04_AI_HARNESS/agent_loops/build_loop.md and project-guardrails.mdc.

Show me your plan before editing files.
```

## Definition of "done" for founder

You don't need to read code. Done when:

- [ ] Agent checked all acceptance criteria in task file
- [ ] You completed manual smoke test for that feature area
- [ ] Human reviewer said "ok to merge" for Critical tasks
- [ ] GitHub issue closed (if using project board)

## What not to do

- Don't ask agent to " refactor everything"
- Don't skip **Now** tasks for visible UI features
- Don't deploy to production without DEBUG=false verification
