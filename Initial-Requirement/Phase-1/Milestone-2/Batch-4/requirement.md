# WB-1.2.4: Platform administration

**Milestone:** MS-1.2 (Subscriptions and platform administration) | **Phase:** PH-1 | **Day:** 4 | **Status:** PLANNED | **Points planned:** 6 | **Budget:** 90% of the day

## Goal
The Super Admin runs the platform: dashboard, announcements, global categories, platform settings, platform reports, activity log and company offboarding.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §3.3 | Platform dashboard (total companies, active vs expired, revenue by plan, new signups, expiring soon); platform reports (revenue, churn, plan distribution) | M |
| §3.3 | Global announcements and maintenance notices shown to all companies | S |
| §3.3, §4.2 | Global category master with compliance profile (Food: FSSAI fields; Packaged: Legal Metrology fields; Other) | S |
| §3.3 | Platform settings: email, SMS and WhatsApp providers, storage, default tax templates, bank verification API settings; keys encrypted and masked | S |
| §3.3 | Super Admin activity log view; company offboarding: export all company data, delete after the agreed retention period | S |

## Depends on
WB-1.2.3, WB-1.1.3 (audit log).

## Deliverables
- Database: `announcements`, `global_categories`, `compliance_profiles`, `platform_settings`, `offboarding_requests`.
- API: Dashboard figures, announcements, global categories, settings, export job, retention deletion job.
- Screens: Super Admin dashboard, announcements, global categories, settings, activity log, offboarding.
- Jobs, integrations: Data export job (zip of CSV and files); scheduled deletion after retention.

## Acceptance criteria
- Given a maintenance notice, when any Company Admin signs in, then it is shown until dismissed.
- Given a company marked for offboarding, when the export finishes, then the Super Admin can download it, and deletion happens only after the retention date.

## Tests
- Dashboard query tests
- Settings encryption tests
- E2E: global category with Food profile

## Out of scope (moves to a later batch)
- Support tickets (Release 2)

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
