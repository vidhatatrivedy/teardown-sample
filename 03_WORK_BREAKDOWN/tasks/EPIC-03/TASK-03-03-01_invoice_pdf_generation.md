# TASK-03-03-01 — Invoice PDF generation

**Epic:** EPIC-03  
**Feature:** FEAT-03-03 Invoice generation  
**Size:** M  
**Priority:** Medium

## Dependencies

TASK-03-01-01

## Context

Frontend uses html2pdf; backend has WeasyPrint path at `GET .../bookings/{id}/invoice`.

## Work

1. Standardize on one approach (recommend backend PDF for consistency)
2. Invoice includes: company name, booking ref, amounts, restaurant bank details
3. Anonymized sample data in tests only

## Acceptance criteria

- [ ] Download invoice PDF for booking
- [ ] PDF opens in browser and prints correctly
- [ ] Missing bank details shows graceful placeholder
