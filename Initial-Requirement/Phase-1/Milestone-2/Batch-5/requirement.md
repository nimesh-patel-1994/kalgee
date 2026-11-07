# WB-1.2.5: Integration: subscriptions and platform (milestone demo)

**Milestone:** MS-1.2 (Subscriptions and platform administration) | **Phase:** PH-1 | **Day:** 5 | **Status:** PLANNED | **Points planned:** 5 | **Budget:** 90% of the day

## Goal
Trial → active → expiring → expired → suspended works with jobs, limits block correctly, payments renew subscriptions, and the demo is ready.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| MS-1.2 | End-to-end subscription journey with a fake clock; payment renewal; limit enforcement across modules built so far | M |
| MS-1.1 regression | Regression of the access milestone; fixes from review | M |
| calibration | Milestone-end recalibration and re-size of the batches not yet started | S |

## Depends on
WB-1.2.1 to WB-1.2.4.

## Deliverables
- Database: —
- API: —
- Screens: Demo script `docs/demo/MS-1.2.md`.
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
