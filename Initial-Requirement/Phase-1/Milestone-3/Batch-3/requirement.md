# WB-1.3.3: Tax master and GST setup

**Milestone:** MS-1.3 (Company setup and master data) | **Phase:** PH-1 | **Day:** 3 | **Status:** PLANNED | **Points planned:** 5 | **Budget:** 90% of the day

## Goal
Tax rates, HSN and company defaults work as specified, and the design keeps other countries possible later.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §4.2 (#), §11 | Country-aware tax master (India GST now; structure allows other tax systems later) | M |
| §4.17 | Company default CGST, SGST and IGST; tax type per product (taxable, nil-rated, exempt, zero-rated); tax-inclusive or tax-exclusive prices per company | S |
| §4.17 | Changing the default updates only products still on the default; option to apply the new default to selected products; audit of every tax rate change | S |
| §4.21 | Place-of-supply service: same state → CGST + SGST, other state → IGST, from GSTIN state codes | S |

## Depends on
WB-1.3.1.

## Deliverables
- Database: `tax_systems`, `tax_rates`, `hsn_codes`, `company_tax_defaults`, `tax_rate_changes`.
- API: Tax master read, company defaults, apply-to-selected, place-of-supply calculation service.
- Screens: Tax settings page; default change dialog with 'apply to selected'.
- Jobs, integrations: —

## Acceptance criteria
- Given default 6% + 6% and a product overridden to 2.5% + 2.5%, when the default becomes 9% + 9%, then only products on the default change.
- Given seller in Gujarat (24) and buyer in Maharashtra (27), when tax is calculated, then IGST applies.

## Tests
- Tax calculation unit tests (inclusive and exclusive)
- Place-of-supply tests
- Audit tests

## Out of scope (moves to a later batch)
- Bill of Supply and reverse charge (Release 2)

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
