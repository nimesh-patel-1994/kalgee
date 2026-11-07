# MS-4.3: Online orders and store management

**Phase:** PH-4 | **Status:** OUTLINE | **Week:** 15 | **Points planned:** 29

## Goal and end-of-week demo
Admin order handling, returns and refunds, store settings and domains, and website content.

## Work batches and how they connect
| Work batch | Title | Depends on | Requirement refs |
|------------|-------|------------|------------------|
| WB-4.3.1 | Online order handling | MS-4.2 (previous milestone) | §5.9 |
| WB-4.3.2 | Returns, refunds and settlement | WB-4.3.1 | §5.9, §5.11 |
| WB-4.3.3 | Store settings and domains | WB-4.3.2 | §5.7, §5.11, §4.18 |
| WB-4.3.4 | Blogs, policies and FAQs | WB-4.3.3 | §5.12 |
| WB-4.3.5 | Integration: orders and store | WB-4.3.4 | MS-4.3 |

```mermaid
flowchart LR
  B1["WB-4.3.1"] --> B2["WB-4.3.2"]
  B2["WB-4.3.2"] --> B3["WB-4.3.3"]
  B3["WB-4.3.3"] --> B4["WB-4.3.4"]
  B4["WB-4.3.4"] --> B5["WB-4.3.5"]
```

## Integration points
Each work batch builds on the tables, endpoints, services and screens of the batch before it (see "Depends on" and "Produces"); the last batch (WB-4.3.5) joins them into one end-to-end journey, runs the regression of earlier milestones and prepares the demo. Shared building blocks used across batches: the tenant filter and authorisation policy (MS-1.1), the audit log (WB-1.1.3), the import framework (WB-1.3.4) and the stock engine (WB-1.4.2).

## Complete requirement of the milestone
Written in detail when the phase becomes ACTIVE (union of the detailed work batches).

**Milestone acceptance:**
- Given the milestone demo script, when the developer follows it, then every step works without manual fixes.

## Specs approval
Gate G2 for this milestone: the specs of all its work batches are approved on day 1; batches then run day by day without stopping except for failures.

## Definition of done (milestone)
Every work batch DONE or carried over with the developer's OK, the integration batch passed (end-to-end journey, smoke, regression of earlier milestones), the demo accepted.
