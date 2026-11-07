# WB-1.1.3: Roles, permissions, staff users and audit trail

**Milestone:** MS-1.1 (Foundation and access) | **Phase:** PH-1 | **Day:** 3 | **Status:** PLANNED | **Points planned:** 6 | **Budget:** 90% of the day

## Goal
Configurable two-level RBAC works end to end, Company Admins manage staff users, and every change is recorded in an audit trail.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §2 | Roles with module × action matrix (view, create, edit, delete, export); Super Admin defines Company Admin roles; Company Admin defines staff roles and cannot grant more than they hold | L |
| §4.16 | Staff management: create, edit, deactivate staff users and assign roles | S |
| §2, §7 | Activity and audit log foundation (who, what, when, old and new values) used by every later module; user profile with photo and contact details | S |

## Depends on
WB-1.1.2 (users, sign-in).

## Deliverables
- Database: `roles`, `role_permissions`, `modules`, `user_roles`, `audit_log`.
- API: Roles CRUD, permission matrix, staff users CRUD, `/me/permissions`, audit log query; authorisation policy per module and action on every endpoint.
- Screens: Roles and permission matrix screen, staff list and form, profile page, menu filtered by permissions.
- Jobs, integrations: —

## Acceptance criteria
- Given a staff role with 'Products: view' only, when that staff member opens Products, then they can view but every create, edit and delete control is hidden and the API returns 403.
- Given a Company Admin whose own role lacks 'export', when they edit a staff role, then 'export' cannot be granted.
- Given any create or edit, when it is saved, then an audit entry shows who, when, and the old and new values.

## Tests
- Permission policy unit tests
- API 403 integration tests per action
- E2E: role creation and restricted menu

## Out of scope (moves to a later batch)
- Statutory staff details and payroll (Phase 3)

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
