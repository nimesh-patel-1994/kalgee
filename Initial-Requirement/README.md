# Kalgee: delivery plan (Release 1)

> Phase → Milestone → Work batch (toolkit 1.5.0, phasing skill). One work batch is one working day and uses at most 90% of the day's usage budget.
> Structure: 4 milestones per phase, 5 work batches per milestone (the 5th is integration, demo and buffer), 5 working days a week.
> Scope: Release 1 of `FeatureListing.md` v1.5 (sections referenced as §n.n): the web system (PH-1 to PH-5) and the ERP Mobile App for staff and owners (PH-6, §14). Release 2 (including the Flutter customer app, §5.14, a separate app) is planned separately.
> Stack: .NET (API), React (Admin Panel and storefront), PostgreSQL, Flutter (ERP Mobile App).
> Written 2026-11-01, PH-6 (mobile) added 2026-11-11. Phase 1 is detailed; later phases are outlines, detailed when they start, after re-planning with the measured points per batch.

## How work batches were sized
- Starting estimate: about **6 points per work batch** (S=1, M=2, L=4), roughly one module end to end: table and migration, API, list and form screens, validation, tests, review and the test loop.
- **WB-1.1.1 to WB-1.1.3 are the calibration batches.** After them, and at the end of every milestone, the measured points per batch re-size every batch that has not started (only with the developer's OK).
- Each milestone's 5th work batch adds no new features: integration journey, regression, fixes, demo. It is the buffer that keeps a weekly milestone reliable.
- UI approach: the admin panel is built as working vertical slices on a design system set up in WB-1.1.1 (Hallmark lint every integration batch); the customer storefront starts UI-first (WB-4.2.1: every store screen prototyped and frozen before it is wired).

## Phases
| Phase | Title | Milestones | Work batches | Status |
|-------|-------|------------|--------------|--------|
| [PH-1](Phase-1/requirement.md) | Platform foundation, tenancy, subscriptions and catalogue | 4 | 20 | PLANNED |
| [PH-2](Phase-2/requirement.md) | Buying, selling and production | 4 | 20 | OUTLINE |
| [PH-3](Phase-3/requirement.md) | Costs, people, exhibitions and GST compliance | 4 | 20 | OUTLINE |
| [PH-4](Phase-4/requirement.md) | eCommerce store | 4 | 20 | OUTLINE |
| [PH-5](Phase-5/requirement.md) | Reports, insights and release readiness | 3 | 15 | OUTLINE |
| [PH-6](Phase-6/requirement.md) | ERP Mobile App (Flutter, Android first then iOS) | 3 | 15 | OUTLINE |
| | **Total** | 22 | **110** (about 22 weeks) | |

The total is an estimate. The web system (PH-1 to PH-5) is 95 work batches (about 19 weeks) and goes live at the end of PH-5; the ERP Mobile App (PH-6, 15 work batches) follows once the web system is complete. It firms up after the calibration batches: if a work batch delivers more than 6 points, phases shrink and merge; if less, they grow.

## Calibration (filled at every batch close-out)
| Work batch | Date | Points planned | Points done | Usage used (% of window) | Points per batch (rolling) | Notes |
|------------|------|----------------|-------------|--------------------------|----------------------------|-------|

## Re-plans
| Date | Why | What moved |
|------|-----|------------|

## ERP Mobile App (PH-6) and mobile-ready APIs
- The ERP Mobile App is for Company Admins and Company Staff only, with the Must and Should features of `FeatureListing.md` §14.2 and §14.3 (about 15 screen groups); heavy set-up and analysis stay on the web (§14.6). Offline works for sales and stall billing and stock scans only; scanning is by camera only.
- It uses the same APIs, rules, permissions and module structure as the web panel. So that PH-6 needs no API rework, every phase from PH-1 builds the mobile-ready conventions of §14.4 (versioned routes, paginated lists, idempotent creates, device sessions and push tokens, offline invoice sync, attachments, push notifications). They are listed in each phase's "Mobile-readiness" section and in the work batches they touch: WB-1.1.1, WB-1.1.2, WB-1.1.5, WB-2.1.2, WB-2.2.1, WB-2.2.2, WB-2.4.2, WB-3.1.1, WB-3.1.3, WB-3.1.4, WB-3.2.3, WB-3.3.2, WB-4.3.1, WB-5.2.4, WB-5.3.1, WB-5.3.2. They add no points; the calibration batches show if any batch needs re-sizing.
- The Flutter customer storefront app (§5.14) is a separate app in Release 2 and is not in this plan.
- Open points before PH-6: iOS needs an Apple developer account and a Mac; offline invoice numbering is agreed with the CA (WB-2.2.2); a Firebase project is needed for push notifications.
