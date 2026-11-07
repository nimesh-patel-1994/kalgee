# WB-1.1.2: Authentication and sessions

**Milestone:** MS-1.1 (Foundation and access) | **Phase:** PH-1 | **Day:** 2 | **Status:** PLANNED | **Points planned:** 6 | **Budget:** 90% of the day

## Goal
Users sign in with email or mobile and password, recover and change their password, and sessions behave as specified.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §2 | Login with email or mobile plus password; JWT access token with refresh token rotation | M |
| §2 | Forgot and reset password by email link; change password | S |
| §2, §13 | Session management: auto-logout after inactivity (default 30 minutes, configurable), list of active sessions, log out one device, log out from all devices | M |
| §7 security | Password hashing (Argon2id or bcrypt), login throttling and lockout, security events in the log | S |

## Depends on
WB-1.1.1 (solution, tenancy base, shell).

## Deliverables
- Database: `users`, `user_sessions`, `password_reset_tokens`.
- API: `/auth/login`, `/auth/refresh`, `/auth/logout`, `/auth/logout-all`, `/auth/sessions`, `/auth/forgot`, `/auth/reset`, `/auth/change-password`.
- Screens: Login, forgot password, reset password, change password, active sessions page; inactivity timer.
- Jobs, integrations: Email sending through a development mail catcher (real provider settings come in WB-1.2.4).

## Acceptance criteria
- Given a user with mobile 98xxxxxxx and a password, when they sign in with the mobile number, then they reach the dashboard.
- Given 5 failed logins, when a 6th is tried within the lock window, then it is refused with a clear message.
- Given two active sessions, when the user chooses 'log out from all devices', then both refresh tokens stop working.
- Given 30 minutes without activity, when the user clicks anything, then they are signed out.

## Tests
- Auth service unit tests
- Token rotation and revocation integration tests
- E2E: login, logout, reset password

## Out of scope (moves to a later batch)
- Two-factor authentication (Release 2)
- Customer (storefront) login (Phase 4)

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
