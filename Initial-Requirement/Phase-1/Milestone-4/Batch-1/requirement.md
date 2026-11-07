# WB-1.4.1: Finished goods product master

**Milestone:** MS-1.4 (Products and the stock engine) | **Phase:** PH-1 | **Day:** 1 | **Status:** PLANNED | **Points planned:** 6 | **Budget:** 90% of the day

## Goal
Products are complete: identity, prices, tax, HSN and the compliance fields their category requires.

## Requirements in this batch
| Ref | Requirement (short) | Size (S=1, M=2, L=4) |
|-----|---------------------|----------------------|
| §4.3 | Product master: name, SKU, barcode, category, unit, images, description, visible on website flag | M |
| §4.3, §13 | Prices: cost, MRP, selling, wholesale; selling price above MRP blocked | S |
| §4.17, §4.21 | Tax pre-filled from the company default, editable; HSN mandatory (at least 4 digits) | S |
| §4.21 | Compliance fields by category profile: Legal Metrology (manufacturer or packer, generic name, net quantity, consumer care, origin) and FSSAI (veg/non-veg, ingredients, nutrition per 100 g/ml, allergens, storage) | M |

## Depends on
WB-1.3.2, WB-1.3.3, file storage from WB-1.2.4.

## Deliverables
- Database: `products`, `product_images`, `product_compliance`.
- API: Products CRUD with images; compliance fields per profile.
- Screens: Product list and form with dynamic compliance section.
- Jobs, integrations: Image resizing.

## Acceptance criteria
- Given a Food category product, when the form opens, then the FSSAI fields appear and are required as specified.
- Given MRP 100 and selling price 105, when saved, then it is refused.
- Given a 3-digit HSN, when saved, then it is refused.

## Tests
- Validation unit tests
- E2E: create a Food product

## Out of scope (moves to a later batch)
- Variants (Release 2)
- Stock (WB-1.4.2)

## Definition of done
Built, reviewed and tested within the batch budget; closed out (statuses, changelog, calibration row with `make-plan.ps1 -Action close`). Anything unfinished is CARRIED-OVER to the next batch with the developer's OK.
