# MS-2.1: Purchasing

**Phase:** PH-2 | **Status:** OUTLINE | **Week:** 5 | **Points planned:** 29

## Goal and end-of-week demo
Purchase orders, goods receipt, purchase bills with input GST, returns and supplier payments.

## Work batches and how they connect
| Work batch | Title | Depends on | Requirement refs |
|------------|-------|------------|------------------|
| WB-2.1.1 | Purchase orders with approval | PH-1 (previous phase) | §4.9, §4.20, §13 |
| WB-2.1.2 | Goods receipt (GRN) | WB-2.1.1 | §4.20, §4.5 |
| WB-2.1.3 | Purchase bills | WB-2.1.2 | §4.9, §4.17 |
| WB-2.1.4 | Purchase returns and supplier payments | WB-2.1.3 | §4.9 |
| WB-2.1.5 | Integration: purchasing | WB-2.1.4 | MS-2.1 |

```mermaid
flowchart LR
  B1["WB-2.1.1"] --> B2["WB-2.1.2"]
  B2["WB-2.1.2"] --> B3["WB-2.1.3"]
  B3["WB-2.1.3"] --> B4["WB-2.1.4"]
  B4["WB-2.1.4"] --> B5["WB-2.1.5"]
```

## Integration points
Each work batch builds on the tables, endpoints, services and screens of the batch before it (see "Depends on" and "Produces"); the last batch (WB-2.1.5) joins them into one end-to-end journey, runs the regression of earlier milestones and prepares the demo. Shared building blocks used across batches: the tenant filter and authorisation policy (MS-1.1), the audit log (WB-1.1.3), the import framework (WB-1.3.4) and the stock engine (WB-1.4.2).

## Complete requirement of the milestone
Written in detail when the phase becomes ACTIVE (union of the detailed work batches).

**Milestone acceptance:**
- Given the milestone demo script, when the developer follows it, then every step works without manual fixes.

## Specs approval
Gate G2 for this milestone: the specs of all its work batches are approved on day 1; batches then run day by day without stopping except for failures.

## Definition of done (milestone)
Every work batch DONE or carried over with the developer's OK, the integration batch passed (end-to-end journey, smoke, regression of earlier milestones), the demo accepted.
