# WB-1.3.5: Integration: company setup and masters (milestone demo)

**Milestone:** MS-1.3 (Company setup and master data) | **Phase:** PH-1 | **Day:** 5 | **Status:** PLANNED | **Points planned:** 5 | **Budget:** 90% of the day

## Goal
A new company is fully set up from zero (settings, Master Configuration, tax, masters by import); regression and demo.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| MS-1.3 | End-to-end company setup journey including imports | M |
| regression | Regression of MS-1.1 and MS-1.2; fixes | M |
| calibration | Milestone-end recalibration | S |

## Depends on
WB-1.3.1 to WB-1.3.4.

## Deliverables
- Database: —
- API: —
- Screens: Demo script `docs/demo/MS-1.3.md`.
- Jobs, integrations: —

## Acceptance criteria
- Given the demo script, when followed, then every step works without manual fixes.

## Tests
- E2E milestone journey
- Regression suite
- Smoke

## Out of scope (moves to a later batch)
- New features

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
