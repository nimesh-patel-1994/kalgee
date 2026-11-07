# WB-1.3.4: Excel/CSV import and export framework

**Milestone:** MS-1.3 (Company setup and master data) | **Phase:** PH-1 | **Day:** 4 | **Status:** PLANNED | **Points planned:** 5 | **Budget:** 90% of the day

## Goal
One reusable import flow (template, upload, preview with row-level validation, fix, confirm) and export, applied to the masters so far.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §4.2, §7 | Import framework: template download, upload, preview with row-level errors, fix and re-validate, confirm; idempotent and audited | M |
| §4.2, §7 | Export of masters to Excel and CSV | S |
| §4.2 | Applied to categories, brands, units and suppliers | M |

## Depends on
WB-1.3.2, WB-1.3.3.

## Deliverables
- Database: `import_jobs`, `import_rows`.
- API: Template, upload, preview, confirm, export endpoints (generic per entity).
- Screens: Import wizard (upload, preview grid with errors, confirm); export buttons.
- Jobs, integrations: Import processing in the background for large files.

## Acceptance criteria
- Given a file with one row naming an unknown unit, when it is previewed, then that row is marked with the error and the others are valid.
- Given a confirmed import, when it is confirmed again, then nothing is imported twice.

## Tests
- Parser and validation unit tests
- Import integration tests
- E2E: import suppliers

## Out of scope (moves to a later batch)
- Product, stock, customer and sales imports (later batches reuse this)

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
