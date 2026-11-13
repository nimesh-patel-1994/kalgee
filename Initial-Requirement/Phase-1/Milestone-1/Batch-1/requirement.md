# WB-1.1.1: Solution skeleton, tenancy base and design system (calibration batch)

**Milestone:** MS-1.1 (Foundation and access) | **Phase:** PH-1 | **Day:** 1 | **Status:** PLANNED | **Points planned:** 6 | **Budget:** 90% of the day

## Goal
An empty but production-shaped solution runs locally with one command: .NET API, PostgreSQL with migrations, React admin shell with the design system, and the multi-tenant base every later table uses.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §1, §9 #40 | Solution layout: .NET API (clean layers: Api, Application, Domain, Infrastructure), EF Core with PostgreSQL migrations, React (Vite, TypeScript) admin app | M |
| §1, §7 security | Multi-tenant base: company id on every tenant-owned table, global query filter, tenant resolution from the signed-in user, cross-tenant guard in the data layer | M |
| §7 responsive UI | Design system: tokens (colours, type, spacing), app shell (header, side menu, content area), responsive layout, `DESIGN.md`; Hallmark lint on the shell | S |
| §7 | Platform plumbing: structured logging, error response format, health endpoint, OpenAPI with a generated TypeScript client, run kit (`start.cmd`), CI workflow, secret scan | S |
| §14.4 | Mobile-ready API conventions: `/v1` versioning, one pagination and field-selection standard for every list, idempotency-key support on create endpoints, server time stamping (absorbed in the platform plumbing item, no extra points; checked at calibration) | — |

## Depends on
None (first batch).

## Deliverables
- Database: Migrations project; base entity (id, company id, created/updated by and at); `companies` table stub.
- API: `/health`; OpenAPI document; problem-details error format.
- Screens: Admin shell with empty dashboard page, side menu, top bar; light theme (dark mode later if agreed).
- Jobs, integrations: `start.cmd` starts PostgreSQL (Docker), API and web; CI builds and tests both.

## Acceptance criteria
- Given a fresh clone, when the developer double-clicks `start.cmd`, then the API health check and the admin shell answer within 2 minutes.
- Given two companies' rows in a tenant table, when a query runs for company A, then no row of company B is returned (automated test).
- Given the design tokens, when the shell is linted by Hallmark, then there is no Floor finding.
- Given any list endpoint, when it is called without paging parameters, then it returns a bounded first page with the paging fields (contract test).
- Given a create request sent twice with the same idempotency key, when both arrive, then exactly one record exists and the second call returns the first result (shared test helper, applied to real endpoints from Phase 2).

## Tests
- Tenant filter unit and integration tests
- API health integration test
- Playwright smoke: shell loads
- CI green

## Out of scope (moves to a later batch)
- Authentication (WB-1.1.2)
- Any business screen

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
