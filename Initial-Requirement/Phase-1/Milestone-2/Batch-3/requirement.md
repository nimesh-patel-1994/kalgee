# WB-1.2.3: Subscription invoices and Razorpay for the platform

**Milestone:** MS-1.2 (Subscriptions and platform administration) | **Phase:** PH-1 | **Day:** 3 | **Status:** PLANNED | **Points planned:** 5 | **Budget:** 90% of the day

## Goal
The Super Admin bills companies with GST tax invoices and collects payment manually or online through the platform's own Razorpay.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §3.2 | GST tax invoice for subscription fees issued by the Super Admin to each company (with company GSTIN), PDF, numbering | M |
| §3.2 | Record manual payments; payment history per company | S |
| §3.2, §9 #25 | Online subscription payment through the Super Admin's Razorpay: order, checkout, webhook with signature check, retry of failed payments, renewal on success | M |

## Depends on
WB-1.2.1 (subscriptions). The platform invoice uses the platform's own GST settings; company tax setup comes in WB-1.3.3.

## Deliverables
- Database: `subscription_invoices`, `subscription_payments`.
- API: Invoice generation and PDF; payment record; Razorpay order and webhook endpoints.
- Screens: Super Admin billing screens; Company Admin 'pay now' and invoice download.
- Jobs, integrations: Invoice on renewal.

## Acceptance criteria
- Given a renewal, when payment succeeds in Razorpay test mode, then the webhook (with a valid signature) marks the invoice paid and extends the subscription.
- Given a webhook with a wrong signature, when it arrives, then it is rejected and logged.

## Tests
- Invoice numbering and tax calculation unit tests
- Webhook signature tests
- E2E with Razorpay test keys

## Out of scope (moves to a later batch)
- Store payments for customers (Phase 4)

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
