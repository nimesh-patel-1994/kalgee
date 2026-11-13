# WB-1.1.5: Integration: foundation and access (milestone demo)

**Milestone:** MS-1.1 (Foundation and access) | **Phase:** PH-1 | **Day:** 5 | **Status:** PLANNED | **Points planned:** 5 | **Budget:** 90% of the day

## Goal
The whole milestone works as one journey, tenant isolation is proven, and the week's demo is ready. No new features.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| MS-1.1 | End-to-end journey: Super Admin creates company → Company Admin signs in → creates a staff role and user → staff member sees only the permitted menu | M |
| §7 security | Cross-tenant tests on every endpoint built so far; Hallmark audit of all screens; fixes from review | M |
| calibration | Close-out of the calibration figures from WB-1.1.1 to WB-1.1.4; re-size the plan if needed | S |

## Depends on
WB-1.1.1 to WB-1.1.4.

## Deliverables
- Database: —
- API: —
- Screens: Demo script `docs/demo/MS-1.1.md`.
- Jobs, integrations: Smoke test covers sign-in.

## Acceptance criteria
- Given the demo script, when the developer follows it, then every step works without manual fixes.
- Given a token of company A, when any company-B id is requested on any endpoint, then the API returns 404 or 403.
- Given the API contract, when the mobile-readiness check runs (versioned routes, paginated lists, idempotent creates, device sessions), then it passes for every endpoint built so far.

## Tests
- E2E milestone journey
- Cross-tenant regression suite
- Smoke

## Out of scope (moves to a later batch)
- New features

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
