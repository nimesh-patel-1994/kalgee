# WB-1.4.3: Raw material, packing and label stock

**Milestone:** MS-1.4 (Products and the stock engine) | **Phase:** PH-1 | **Day:** 3 | **Status:** PLANNED | **Points planned:** 5 | **Budget:** 90% of the day

## Goal
Raw material, packing material and labels have their masters and stock through the same engine.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §4.4 | Raw material master (name, code, unit, category, supplier, price); price history (latest and average); wastage and spoilage | M |
| §4.7 | Packing items master with price; stock in/out, adjustments, ledger | S |
| §4.8 | Label master (per product, size, language) with price and design reference; stock, ledger; label-wise wastage and misprints | M |

## Depends on
WB-1.4.2.

## Deliverables
- Database: `raw_materials`, `packing_items`, `labels`, `price_history`.
- API: CRUD per master; stock in/out through the engine; wastage entries.
- Screens: Three masters with stock views and wastage entry.
- Jobs, integrations: —

## Acceptance criteria
- Given purchases at 50 and 60, when the price history is shown, then latest is 60 and average follows the quantities.
- Given 20 labels misprinted, when recorded, then label stock falls by 20 and the wastage report lists them.

## Tests
- Price history tests
- Engine integration tests per stock type

## Out of scope (moves to a later batch)
- BOM links (Phase 2 production)

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
