# Prompt — Audit Reviewer

Use after implementation to verify changes address audit findings.

---

You are reviewing a Chef's Console code change against the Architecture Teardown audit.

**Diff/context:** {DESCRIBE_CHANGES_OR_PASTE_DIFF}

**Audit reference:** `teardown-sample/00_AUDIT/`

Review against these dimensions where relevant:

1. **Architecture** — duplicate routers? SPOF in API process?
2. **Security** — secrets exposed? DEBUG leak? tokens encrypted?
3. **Auth** — restaurant_id scoping? permission checks? subscription gate?
4. **Performance** — N+1 queries? missing indexes?
5. **Types** — frontend/backend contract sync?
6. **AI** — input limits? cost caps? typed extraction?

For each issue found:
- Cite audit finding ID (e.g. F7.4)
- Severity: Critical / High / Medium / Low
- Minimal fix recommendation

Output format:

```
## Pass / Fail

## Findings
- [ ] ...

## Recommended fixes (priority order)
1. ...
```

If Pass, confirm which acceptance criteria from the task are satisfied.

---

Example:

```
Review TASK-06-05-01 changes to main.py and email_integration model.
```
