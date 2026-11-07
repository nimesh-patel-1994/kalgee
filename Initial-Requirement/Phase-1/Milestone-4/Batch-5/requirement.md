# WB-1.4.5: Integration: products and stock (milestone demo and phase gate)

**Milestone:** MS-1.4 (Products and the stock engine) | **Phase:** PH-1 | **Day:** 5 | **Status:** PLANNED | **Points planned:** 5 | **Budget:** 90% of the day

## Goal
Products and stock work as one journey; Phase 1 is demonstrated and accepted at gate G-P; Phase 2 is re-planned with the measured points per batch.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| MS-1.4 | Journey: product setup → opening stock → adjustments with approval → valuation → alerts | M |
| Phase 1 regression | Full regression of Phase 1, cross-tenant suite, Hallmark audit, `/security-audit` scanners | M |
| calibration | Phase gate: calibration, re-plan Phase 2 in detail | S |

## Depends on
WB-1.4.1 to WB-1.4.4.

## Deliverables
- Database: —
- API: —
- Screens: Demo script `docs/demo/PH-1.md`.
- Jobs, integrations: —

## Acceptance criteria
- Given the Phase 1 demo script, when followed, then every step works and the developer accepts the phase.

## Tests
- Phase regression
- Smoke
- Security scanners

## Out of scope (moves to a later batch)
- New features

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
