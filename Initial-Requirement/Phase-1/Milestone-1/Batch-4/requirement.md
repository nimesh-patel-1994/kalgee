# WB-1.1.4: Company (tenant) management by the Super Admin

**Milestone:** MS-1.1 (Foundation and access) | **Phase:** PH-1 | **Day:** 4 | **Status:** PLANNED | **Points planned:** 6 | **Budget:** 90% of the day

## Goal
The Super Admin creates and manages companies, each with one GSTIN, one PAN and exactly one Company Admin, and can act as a company with a full audit trail.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §3.1 | Company CRUD with profile (name, logo, GSTIN, PAN, address, contact, currency, timezone, financial-year start); suspend, reactivate, delete (soft) | M |
| §3.1, §4.21 | One GSTIN and one PAN per company, unique across the platform; GSTIN format check and state code; correction only by the Super Admin with audit | M |
| §3.1 | Create the single Company Admin; reset Admin credentials; enforce one Admin per company; company status Trial, Active, Expired, Suspended | S |
| §3.1 | 'Login as' a company with every Super Admin action audited; company usage overview (users, products, orders, storage) with counters | S |

## Depends on
WB-1.1.3 (roles, audit log).

## Deliverables
- Database: `companies` (complete), `company_status_history`.
- API: Companies CRUD and status actions, create or reset Company Admin, impersonation start and end, usage overview.
- Screens: Super Admin: company list with filters, company form, status actions, 'login as' banner while impersonating.
- Jobs, integrations: —

## Acceptance criteria
- Given a company with GSTIN 24AAAAA0000A1Z5, when another company is created with the same GSTIN, then it is refused.
- Given an invalid GSTIN format, when the form is saved, then the field shows the error and nothing is saved.
- Given a company that already has an Admin, when a second Admin is created, then it is refused.
- Given the Super Admin uses 'login as', when they change a record, then the audit entry names the Super Admin and the company.

## Tests
- GSTIN validator unit tests (format, checksum, state code)
- Uniqueness integration tests
- E2E: create company and its Admin, log in as the Admin

## Out of scope (moves to a later batch)
- Subscription plans (WB-1.2.1)

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
