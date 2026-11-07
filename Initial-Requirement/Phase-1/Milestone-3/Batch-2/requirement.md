# WB-1.3.2: Catalogue masters

**Milestone:** MS-1.3 (Company setup and master data) | **Phase:** PH-1 | **Day:** 2 | **Status:** PLANNED | **Points planned:** 5 | **Budget:** 90% of the day

## Goal
Categories, brands, units and suppliers are maintained per company, with global categories shared and compliance profiles applied.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §4.2, §9 #19 | Categories and sub-categories: global (Super Admin) and company-own; each with a compliance profile | S |
| §4.2 | Brands | S |
| §4.2 | Units of measure with conversions (kg/g, litre/ml, pcs/box) | S |
| §4.2, §4.21 | Suppliers/vendors with contact, payment terms and GSTIN (format check, state code) | M |

## Depends on
WB-1.2.4 (global categories), WB-1.3.1.

## Deliverables
- Database: `categories`, `brands`, `units`, `unit_conversions`, `suppliers`.
- API: CRUD for each master, with search and paging.
- Screens: Masters screens with list, search, form.
- Jobs, integrations: —

## Acceptance criteria
- Given a global Food category, when a company lists categories, then it sees the global ones and its own, and cannot edit the global ones.
- Given 1 box = 12 pcs, when 2 boxes are converted, then the result is 24 pcs.

## Tests
- Unit conversion tests
- Category visibility tests
- E2E: supplier with GSTIN

## Out of scope (moves to a later batch)
- Warehouses and locations (Release 2)

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
