# WB-1.3.1: Company settings and Master Configuration

**Milestone:** MS-1.3 (Company setup and master data) | **Phase:** PH-1 | **Day:** 1 | **Status:** PLANNED | **Points planned:** 6 | **Budget:** 90% of the day

## Goal
The Company Admin sets up the company and switches modules and channels on and off from one Master Configuration table, with keys stored safely.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §4.16 | Company profile, logo, tax details, bank details, invoice template choice and numbering settings; alert thresholds and notification preferences; stock rules shown (FEFO fixed, no negative stock); RMC price basis | M |
| §4.16 | Master Configuration table with on/off toggles and key fields: messaging channels, store Razorpay keys, COD, custom domain, Production/RMC module, default company tax, CA contact and monthly CA on/off, salary in CA pack, Payroll on/off, eCommerce settings placeholder; a feature stays inactive until valid keys are saved | M |
| §4.16, §7.1 | Keys encrypted at rest and shown masked; access to them logged | S |
| §4.16 | Subscription view for the company: current plan, usage vs limits, renewal date, invoices | S |

## Depends on
WB-1.2.2 (limits, usage), WB-1.2.3 (invoices).

## Deliverables
- Database: `company_settings`, `master_configuration`, `secret_values` (encrypted).
- API: Settings and Master Configuration endpoints; masked read; key validation hooks per provider (stubs where the provider comes later).
- Screens: Company settings tabs; Master Configuration table; subscription page.
- Jobs, integrations: —

## Acceptance criteria
- Given WhatsApp switched on without keys, when the Admin saves, then it stays inactive and says keys are needed.
- Given saved keys, when the settings page is reloaded, then only the last 4 characters are visible.

## Tests
- Encryption and masking tests
- Toggle rules tests
- E2E: Master Configuration

## Out of scope (moves to a later batch)
- The providers themselves (messaging in Phase 2, store payments in Phase 4)

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
