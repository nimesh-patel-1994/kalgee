# WB-1.4.4: Alerts, valuation, barcodes and product import

**Milestone:** MS-1.4 (Products and the stock engine) | **Phase:** PH-1 | **Day:** 4 | **Status:** PLANNED | **Points planned:** 6 | **Budget:** 90% of the day

## Goal
Low-stock and expiry alerts, stock valuation, barcode printing and bulk product and tax import complete the stock foundation.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §4.3, §4.4 | Minimum stock and reorder alerts for every stock type | S |
| §4.5 | Expiry alerts at 30, 15 and 7 days (configurable); batch-wise stock and expiry view | S |
| §4.3 | Stock valuation at cost and at selling price | S |
| §4.3, §7 | Barcode and QR generation and printing (labels) | S |
| §4.17, §4.21 | Bulk product import with HSN and tax rates, through the import framework | M |

## Depends on
WB-1.4.2, WB-1.4.3, WB-1.3.4.

## Deliverables
- Database: `alert_rules`, `alerts`.
- API: Alerts list; valuation; barcode image and label PDF; product import.
- Screens: Alert list and dashboard widgets (low stock, expiring); valuation view; print labels dialog.
- Jobs, integrations: Daily alert job.

## Acceptance criteria
- Given a minimum of 10 and stock falling to 9, when the alert job runs, then a low-stock alert appears once.
- Given an import row without HSN, when previewed, then it is marked invalid.

## Tests
- Alert job tests
- Valuation tests
- E2E: print a barcode label

## Out of scope (moves to a later batch)
- Reorder to draft PO (Phase 2)

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
