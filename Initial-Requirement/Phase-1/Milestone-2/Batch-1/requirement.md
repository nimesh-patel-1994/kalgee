# WB-1.2.1: Plans and subscription lifecycle

**Milestone:** MS-1.2 (Subscriptions and platform administration) | **Phase:** PH-1 | **Day:** 1 | **Status:** PLANNED | **Points planned:** 6 | **Budget:** 90% of the day

## Goal
The Super Admin defines plans and runs each company's subscription through its whole life, with automatic expiry and suspension.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §3.2, §9 #24 | Two plan types (Inventory Panel only; Inventory Panel + eCommerce Website), each with weekly, monthly and yearly plans: price, cycle, trial days, limits (staff, products, orders per month, eCommerce on/off, modules) | M |
| §3.2 | Assign, upgrade, downgrade, renew, pause and cancel a company's plan; start and end dates, grace period | M |
| §3.2 | Background jobs: auto-expiry and auto-suspension after the grace period; company status follows | M |

## Depends on
WB-1.1.4 (companies, status).

## Deliverables
- Database: `plans`, `plan_limits`, `subscriptions`, `subscription_events`.
- API: Plans CRUD; subscription actions; subscription history per company.
- Screens: Super Admin: plan list and form, company subscription panel with actions and history.
- Jobs, integrations: Scheduled job runner (for example Hangfire or Quartz, decided in the batch's tech spec) with the daily expiry job.

## Acceptance criteria
- Given a monthly plan ending today with 3 grace days, when the daily job runs on day 4 after the end, then the company becomes Suspended and its users cannot sign in.
- Given an upgrade mid-cycle, when it is saved, then the new limits apply at once and the change is in the history.

## Tests
- Lifecycle state machine unit tests
- Job tests with a fake clock
- E2E: assign plan, upgrade, renew

## Out of scope (moves to a later batch)
- Coupons on plans (Release 2)
- Payments (WB-1.2.3)

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
