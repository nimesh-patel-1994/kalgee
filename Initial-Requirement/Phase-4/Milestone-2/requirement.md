# MS-4.2: Storefront website

**Phase:** PH-4 | **Status:** OUTLINE | **Week:** 14 | **Points planned:** 29

## Goal and end-of-week demo
The common store design with company branding, catalogue, checkout and the customer account.

## Work batches and how they connect
| Work batch | Title | Depends on | Requirement refs |
|------------|-------|------------|------------------|
| WB-4.2.1 | Store design and prototype (UI-first) | MS-4.1 (previous milestone) | §5.7, §5.10, §9 #6 |
| WB-4.2.2 | Catalogue pages | WB-4.2.1 | §5.2, §5.3, §5.10 |
| WB-4.2.3 | Cart and checkout | WB-4.2.2 | §5.4, §5.1, §5.10 |
| WB-4.2.4 | Customer account | WB-4.2.3 | §5.1, §5.5, §5.6, §5.10 |
| WB-4.2.5 | Integration: storefront website | WB-4.2.4 | MS-4.2, §5.11 |

```mermaid
flowchart LR
  B1["WB-4.2.1"] --> B2["WB-4.2.2"]
  B2["WB-4.2.2"] --> B3["WB-4.2.3"]
  B3["WB-4.2.3"] --> B4["WB-4.2.4"]
  B4["WB-4.2.4"] --> B5["WB-4.2.5"]
```

## Integration points
Each work batch builds on the tables, endpoints, services and screens of the batch before it (see "Depends on" and "Produces"); the last batch (WB-4.2.5) joins them into one end-to-end journey, runs the regression of earlier milestones and prepares the demo. Shared building blocks used across batches: the tenant filter and authorisation policy (MS-1.1), the audit log (WB-1.1.3), the import framework (WB-1.3.4) and the stock engine (WB-1.4.2).

## Complete requirement of the milestone
Written in detail when the phase becomes ACTIVE (union of the detailed work batches).

**Milestone acceptance:**
- Given the milestone demo script, when the developer follows it, then every step works without manual fixes.

## Specs approval
Gate G2 for this milestone: the specs of all its work batches are approved on day 1; batches then run day by day without stopping except for failures.

## Definition of done (milestone)
Every work batch DONE or carried over with the developer's OK, the integration batch passed (end-to-end journey, smoke, regression of earlier milestones), the demo accepted.
