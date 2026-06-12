# TASK-03-04-01 — Orders calendar FullCalendar integration

**Epic:** EPIC-03  
**Feature:** FEAT-03-04 Orders calendar  
**Size:** M  
**Priority:** Medium

## Dependencies

TASK-02-03-01

## Context

`/dashboard/orders-calendar` uses FullCalendar with `GET .../orders/calendar/events`.

## Work

1. Verify events include delivery_date, time, booking_reference in title
2. Click event navigates to order detail or booking
3. Timezone from restaurant settings applied

## Acceptance criteria

- [ ] Calendar shows orders for selected restaurant only
- [ ] Month/week view toggle works
- [ ] Empty state when no orders in range
