# Kalgee: delivery plan (Release 1)

> Phase → Milestone → Work batch (toolkit 1.5.0, phasing skill). One work batch is one working day and uses at most 90% of the day's usage budget.
> Structure: 4 milestones per phase, 5 work batches per milestone (the 5th is integration, demo and buffer), 5 working days a week.
> Scope: Release 1 of `FeatureListing.md` v1.4 (sections referenced as §n.n). Release 2 (including the Flutter customer app) is planned separately.
> Stack: .NET (API), React (Admin Panel and storefront), PostgreSQL.
> Written 2026-11-01. Phase 1 is detailed; later phases are outlines, detailed when they start, after re-planning with the measured points per batch.

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
| | **Total** | 19 | **95** (about 19 weeks) | |

The total is an estimate. It firms up after the calibration batches: if a work batch delivers more than 6 points, phases shrink and merge; if less, they grow.

## Calibration (filled at every batch close-out)
| Work batch | Date | Points planned | Points done | Usage used (% of window) | Points per batch (rolling) | Notes |
|------------|------|----------------|-------------|--------------------------|----------------------------|-------|

## Re-plans
| Date | Why | What moved |
|------|-----|------------|
