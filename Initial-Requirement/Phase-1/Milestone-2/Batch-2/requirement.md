# WB-1.2.2: Plan limits, fair-use metering and notifications foundation

**Milestone:** MS-1.2 (Subscriptions and platform administration) | **Phase:** PH-1 | **Day:** 2 | **Status:** PLANNED | **Points planned:** 5 | **Budget:** 90% of the day

## Goal
Plan limits are enforced everywhere, each company's API use is metered and fairly limited, and the platform can notify users in-app and by email.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §3.2 | Enforce limits: number of staff, products, orders per month, eCommerce on/off, enabled modules (menu and API) | M |
| §3.3 | API fair-use limits and usage metering per company, so one company cannot slow down the others | S |
| §7, §3.2 | Notification service: in-app notifications (bell, list, read state) and email; subscription expiry reminders to the Company Admin (in-app and email) | M |

## Depends on
WB-1.2.1 (plans and limits).

## Deliverables
- Database: `usage_counters`, `notifications`, `notification_preferences`.
- API: Limit checks as a shared service; notifications list and mark-read; rate limiting middleware.
- Screens: Notification bell and list; limit-reached messages; usage overview fed by counters.
- Jobs, integrations: Reminder job (7, 3 and 1 days before expiry).

## Acceptance criteria
- Given a plan with 5 staff, when the Company Admin creates the 6th staff user, then it is refused with the limit and an upgrade hint.
- Given a company over its request rate, when it calls again, then it receives 429 while other companies are unaffected.
- Given a subscription expiring in 3 days, when the reminder job runs, then the Company Admin gets an in-app and an email reminder.

## Tests
- Limit service unit tests
- Rate limit integration test across two companies
- Reminder job test

## Out of scope (moves to a later batch)
- SMS and WhatsApp channels (Phase 2)

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
