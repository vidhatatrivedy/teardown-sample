# Agent Loop — Review

Run before every commit or PR. Takes ~5 minutes.

## Security checklist

- [ ] No `.env`, credentials, or API keys in diff
- [ ] New/modified routes use `require_permission` and `verify_restaurant_access`
- [ ] Queries filter by `restaurant_id` from URL — not from user document alone
- [ ] No `str(exception)` returned to HTTP client
- [ ] No new standalone routers duplicating scoped resources

## Architecture checklist

- [ ] Change matches [02_BUILD_SPEC/system_design.md](../../02_BUILD_SPEC/system_design.md)
- [ ] Types updated in backend Pydantic AND frontend (or generated types)
- [ ] No new god-files — split if adding >100 lines to `api.ts`

## Quality checklist

- [ ] Tests added or updated for behavior change
- [ ] Lint passes in affected package
- [ ] No commented-out code blocks left behind
- [ ] Error messages actionable for end user

## Audit regression

If task is in EPIC-06, verify it addresses specific audit finding:

| Task | Audit |
|------|-------|
| TASK-06-01-01 | 07 F7.4, 01 F1.3 |
| TASK-06-05-01 | 06 F6.1, F6.3 |
| TASK-06-03-01 | 02 F2.3 |
| TASK-04-02-01 | 05 F5.1 |

## Prompt for self-review

```
Review my diff against teardown-sample/04_AI_HARNESS/agent_loops/review_loop.md.
List any failures and suggest minimal fixes.
```

## Outcome

- **Pass:** Proceed to commit
- **Fail:** Fix issues, re-run loop — do not commit
