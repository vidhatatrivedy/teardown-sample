# TASK-02-02-02 — Client match-or-suggest after extraction

**Epic:** EPIC-02  
**Feature:** FEAT-02-02  
**Size:** S  
**Priority:** Medium

## Dependencies

TASK-02-02-01, TASK-05-03-01

## Context

`POST /clients/match-or-suggest` matches company name from extraction to existing clients.

## Work

1. Wire extraction UI to call match endpoint
2. Show top 3 suggestions with confidence
3. Allow manual client picker override

## Acceptance criteria

- [ ] Known client "Acme Catering Ltd" suggests correct match
- [ ] Unknown company shows create-new-client shortcut
- [ ] Selected client_id passed to enquiry create
