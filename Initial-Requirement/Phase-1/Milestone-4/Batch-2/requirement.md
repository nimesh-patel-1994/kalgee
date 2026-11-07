# WB-1.4.2: Stock engine: lots, batches, ledger, FEFO and no negative stock

**Milestone:** MS-1.4 (Products and the stock engine) | **Phase:** PH-1 | **Day:** 2 | **Status:** PLANNED | **Points planned:** 7 | **Budget:** 90% of the day

## Goal
One stock engine for every stock type: lots and batches, a movement ledger, FEFO allocation and a concurrency-safe no-negative-stock rule, with opening stock and adjustments.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §4.4, §4.5, §4.18 | Inventory lots (raw material) and batches (finished goods) with quantity, price per unit, supplier, manufacturing and expiry dates | M |
| §4.3, §4.5 | Stock movement ledger with source (purchase, sale, production, return, adjustment, issue); FEFO allocation service | M |
| §4.3, §9 #8 | Negative stock never allowed, safe under concurrent requests | M |
| §4.3, §4.20 | Opening stock entry; adjustments with reason; adjustments above a set value need Company Admin approval | S |

## Depends on
WB-1.4.1.

## Deliverables
- Database: `stock_items`, `inventory_lots`, `stock_batches`, `stock_movements`, `stock_adjustments`, `approval_requests`.
- API: Opening stock, adjustments with approval, stock on hand per item and batch, allocation preview (FEFO).
- Screens: Opening stock entry, adjustment form, approval inbox, stock on hand by batch.
- Jobs, integrations: —

## Acceptance criteria
- Given batches expiring 10 Jan and 20 Jan, when 5 units are allocated, then the 10 Jan batch is used first.
- Given 3 units on hand, when two requests for 2 units arrive at the same time, then exactly one succeeds.
- Given an adjustment above the approval value, when it is saved, then stock changes only after the Admin approves it.

## Tests
- FEFO and allocation unit tests
- Concurrency integration test
- Ledger balance property test

## Out of scope (moves to a later batch)
- Purchases, sales and production postings (Phase 2)

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
