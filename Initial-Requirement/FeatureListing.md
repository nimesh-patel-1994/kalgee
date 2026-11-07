# Multi-Tenant Inventory Management Platform: Feature Listing

**Version:** 1.4 (Release 1/2 naming, technology, Flutter app in Release 2) | **Date:** 01 Nov 2026 | **Status:** Ready for freeze

This document lists every feature planned for the platform. Once it is frozen, the Technical Document will be written. Features I suggested beyond the original brief have been accepted and are now regular requirements (listed with details in Section 13). Items marked **(#)** are design notes rather than user-visible features (see Section 11). Items marked **(###)** are future expansions that are not built now. Every item without a tag is part of Release 1 (first release). Items tagged **[Release 2]** are in scope but planned after the first release. The release tags on accepted suggestions and Compliance items are confirmed. Items marked **[Compliance]** come from Indian regulations found in research (see Section 12) and must be confirmed with your CA or legal advisor. Everything else comes directly from the brief or your answers.

---

## 1. Product Overview

**Two products in one platform:**

1. **Admin Panel:** one shared web panel used by the Super Admin, Company Admins and Company Staff to run inventory, purchasing, sales, expenses, marketing and exhibitions.
2. **eCommerce Website (one per company):** a separate customer-facing store for each company, powered by APIs exposed by the platform. Each store shows that company's products only.

**Tenancy model:** 1 Super Admin, many Companies, exactly 1 Admin per Company, many Staff per Company. All company data is fully isolated.

**Scale assumption:** about 10 companies at launch, with 50 to 60 products per company.

**Customer mobile app (Release 2):** a Flutter app for each company's eCommerce store, using the same storefront APIs (see 5.14).

**Technology:** .NET for the backend and APIs, React for the Admin Panel and the storefront website, PostgreSQL as the database; Flutter for the Release 2 mobile app.

---

## 2. Users and Roles

| Role | Scope | Summary of access |
|---|---|---|
| Super Admin | Whole platform | Full access to everything: manages companies, subscriptions, plans, platform settings, and can view and manage any company's business data. Configures roles and access for Company Admins. |
| Company Admin | Own company | Full access to own company data, staff, settings, reports, eCommerce configuration. Configures roles and access for own Staff. |
| Company Staff | Own company | Access limited by permissions the Company Admin grants. Every staff member can also view their own salary slips and update their own bank details. |
| Chartered Accountant (CA) | Assigned company | Read-only access to that company's invoices, bills, expense and GST ledger reports (Release 2). |
| Customer | Own company's website | Registers and orders from that company's eCommerce site only. |

**Features**
- Configurable role-based access control (RBAC) at two levels: the **Super Admin** defines roles and module access for Company Admins; the **Company Admin** defines roles and module access for own Company Staff (view / create / edit / delete / export per module). A Company Admin cannot grant more than they hold themselves.
- Login with email or mobile plus password; forgot/reset password; change password.
- Session management, auto-logout on inactivity, single-device logout **[Release 1]**.
- Activity/audit log of who did what and when.
- User profile with photo and contact details.

---

## 3. Super Admin Features

### 3.1 Company (Tenant) Management
- Create, edit, suspend, reactivate and delete companies.
- Company profile: name, logo, GST/tax number, address, contact, currency, timezone, financial-year start.
- Each company has exactly one GSTIN and one PAN; more cannot be added. A GSTIN or PAN can belong to only one company on the platform. A business with another GSTIN or PAN is set up as a new company with its own Admin, subscription and data. A wrong number can be corrected only by the Super Admin, with an audit trail.
- Create the single Company Admin for each company; reset Admin credentials.
- Company status: Trial, Active, Expired, Suspended.
- Enforce one Admin per company.
- Company-wise usage overview: users, products, orders, storage.
- Full access to any company's data and screens (view and manage), including "login as" a company, with an audit trail of every Super Admin action.

### 3.2 Subscription Management
- Two plan types, each with its own plans: **Inventory Panel only**, and **Inventory Panel + eCommerce Website**. The eCommerce website, its APIs, blogs, feedback and storefront settings are available only on the second type.
- Plans with billing cycles **Weekly, Monthly, Yearly** for each plan type.
- Plan definition: price, cycle, trial days, and limits (number of staff, products, orders per month, eCommerce website on/off, modules enabled).
- Assign, upgrade, downgrade, renew, pause and cancel a company's plan.
- Start and end dates, grace period, auto-expiry and auto-suspension.
- Expiry reminders to company Admin (in-app and email).
- GST tax invoices for subscription fees issued by the Super Admin to each company (with company GSTIN), payment history; record manual payments.
- Online subscription payment through **Razorpay**, in addition to manual payment recording.
- Coupons/discounts on plans **[Release 2]**.

### 3.3 Platform Administration
- Platform dashboard: total companies, active vs expired, revenue by plan, new signups, expiring soon.
- Global announcements and maintenance notices to all companies.
- Global category master: create categories, with their compliance profile, that every company can use.
- Platform settings: email/SMS/WhatsApp providers, storage, default tax templates.
- Platform-level reports (revenue, churn, plan distribution).
- Super Admin activity log.
- Role and access management: create roles and set module-level permissions for Company Admins.
- API fair-use limits and usage metering per company, so one company cannot slow down the others.
- Platform settings for the third-party bank verification API used for staff bank details.
- Company offboarding: export all company data, then delete after an agreed retention period.
- Support tickets from Company Admins to the Super Admin, with status tracking **[Release 2]**.

---

## 4. Company Admin Panel: Core Modules

### 4.1 Dashboard
- Today's sales, purchases, expenses and profit snapshot.
- Low-stock and expiring-batch alerts.
- Turnover alert: when the financial-year turnover crosses ₹4.5 crore, a popup asks the Admin to prepare 6-digit HSN codes (see 4.21).
- Pending online orders, recent sales, top-selling products.
- Sales trend chart (daily/weekly/monthly).
- Upcoming exhibitions and pending payments (receivable/payable).
- On the 1st of each month: a popup asks the Company Admin to send the previous month's GST and tax invoices to the CA (see 4.17).

### 4.2 Master Data
- Product categories, sub-categories, brands. Categories are added by the Super Admin (shared with all companies) and by each Company Admin (own company only). Each category carries a compliance profile (for example Food: FSSAI fields; Packaged goods: Legal Metrology fields; Other: no extra fields), so the right fields appear when a product is added.
- Units of measure with conversions (kg/g, litre/ml, pcs/box).
- Tax/GST rates and HSN codes, kept in a country-aware tax master (#). Company-level default tax with per-product override (see 4.17).
- Suppliers/vendors with contact and payment terms.
- Warehouses/storage locations **[Release 2]**.
- Bulk import/export of masters via Excel/CSV.

### 4.3 Finished Goods Stock (with price)
- Finished product master: name, SKU, barcode, category, unit, images, description, and compliance fields (see 4.21).
- Price fields: cost price, MRP, selling price, wholesale price **[Release 1]**, CGST/SGST/IGST (pre-filled from the company default, editable per product; see 4.17).
- Current stock per product (and per location if enabled).
- Opening stock entry.
- Negative stock is never allowed: any sale, production or issue that exceeds available stock is blocked with a clear message.
- Stock adjustments (add/reduce) with reason.
- Stock movement ledger (in/out with source: purchase, sale, production, return, adjustment).
- Minimum stock level and reorder alerts.
- Stock valuation (at cost and at selling price).
- Barcode/QR generation and printing.
- Product variants (size, flavour, pack) **[Release 2]**.
- Mark product visible/hidden on eCommerce website; products with zero stock automatically show as "Currently out of stock".

### 4.4 Raw Material Stock (with price)
- Raw material master: name, code, unit, category, supplier, price.
- Current stock, opening stock, adjustments, movement ledger.
- Price history per raw material (latest and average purchase price).
- **Inventory lots:** each opening-stock or purchase entry is a lot with its own lot number, quantity, price per unit, supplier and expiry date. Stock, cost and expiry are tracked lot by lot (see 4.18).
- Minimum stock and reorder alerts.
- Stock valuation.
- Wastage/spoilage recording.

### 4.5 Batch Inventory (with price)
- Batch/lot creation for finished goods and raw materials.
- Batch fields: batch number, manufacturing date, expiry date, quantity, cost per unit, selling price.
- Batch-wise stock on hand and batch-wise price.
- Terminology: a raw material entry is an **inventory lot**; a **batch** is one production run of finished product (see 4.18). Finished goods bought from suppliers get a batch on purchase receipt.
- Stock is always consumed by **FEFO** (First Expired, First Out): the batch closest to expiry is used first for sales, exhibition issues and production.
- Expiry alerts (30/15/7 days, configurable) and expired-stock report.
- Batch traceability: raw-material batches used → finished batch → customers sold to.
- Batch-wise sale and purchase price visibility on bills.

### 4.6 Production and Product RMC (Raw Material Cost)
- **Switchable per company:** the Company Admin can turn the Production/RMC module on or off in Master Configuration (for companies that only trade and do not manufacture). When off, BOM, RMC, production entry and production reports are hidden. The complete batch flow is in 4.18.
- **Recipe / Bill of Materials (BOM)** per product: raw materials, quantities, packing and label used.
- **RMC calculation** per product: sum of raw material cost per unit, using latest, average or batch-actual price (selectable).
- Extended product cost: RMC + packing + label + labour + electricity + other overhead = **total cost per unit**.
- Margin calculation: selling price vs total cost, margin % and markup %.
- Production entry: see 4.18 (raw material is deducted when a batch is created; packing and labels are deducted at the packing stage).
- Yield and wastage tracking (expected vs actual output).
- RMC change history when raw material prices change.
- Alert when a price change makes a product margin fall below a set threshold **[Release 2]**.

### 4.7 Packing Material Stock
- Packing items master (boxes, pouches, bottles, caps, cartons, etc.) with price.
- Stock in/out, adjustments, ledger, low-stock alerts, valuation.
- Link packing items to product BOM for automatic deduction.

### 4.8 Label Stock
- Label master (per product/size/language) with price and design reference.
- Stock in/out, adjustments, ledger, low-stock alerts, valuation.
- Link labels to product BOM for automatic deduction.
- Label printing pulls batch number, manufacturing date, expiry date and MRP from the batch (see 4.18).
- Track label-wise wastage/misprints.

### 4.9 Purchase Management
- Purchase order (PO) creation and approval **[Release 1]**.
- **Purchase bill** entry: supplier, date, items (raw material, packing, label, finished goods), quantity, rate, tax, discount, freight, other charges.
- Auto-update stock and batch on saving the bill.
- Input GST (CGST/SGST/IGST) captured per line with supplier GSTIN; feeds the input tax credit in the monthly GST ledger (see 4.17).
- Attach supplier bill image/PDF.
- Purchase return / debit note.
- Supplier payments: full, partial, advance; payment mode; outstanding balance.
- Supplier ledger and payable ageing.
- Print/download bill (PDF).

### 4.10 Sales Management
- **Sales bill/invoice** creation: customer, date, items with batch selection, quantity, rate, discount, tax, other charges.
- Auto-deduct stock (batch-wise, FEFO) on saving; a bill cannot be saved if it would make stock negative.
- **GST tax invoice (#):** seller and buyer GSTIN, HSN code, place of supply, CGST + SGST for same-state and IGST for inter-state sales, tax-wise totals, amount in words.
- **Invoice type:** every sales invoice is tagged B2B or B2C and the tag stays on the invoice; Export is a future expansion (###) (see 4.17).
- Invoice numbering series (configurable prefix, financial-year reset).
- Bill types: cash, credit, wholesale, retail, exhibition sale, online order.
- Payment received: full, partial, advance; payment mode (cash, UPI, card, bank, cheque).
- Sales return / credit note.
- Quotations/estimates and convert to invoice **[Release 2]**.
- Print (A4 and thermal), download PDF, share by WhatsApp/email/SMS.
- Customer ledger and receivable ageing.
- Online orders appear here and convert to sales bills.
- **Bulk import of orders/sales bills from Excel:** download a template, upload the file, preview with row-level validation (unknown product, insufficient stock, invalid GST), fix errors, then confirm the import. The reading method (for example a Python script) is decided in the Technical Document.
- Company-branded invoice template (logo, terms, bank details, QR).

### 4.11 Customer Management (Customer Contact Details)
- Customer master: name, mobile, email, alternate contact, addresses (billing/shipping), GST number, birthday/anniversary, notes, tags/groups.
- Customer types: retail, wholesale, exhibition lead, online.
- Source tracking: walk-in, online, exhibition, referral.
- Purchase history, lifetime value, outstanding balance.
- Customer segments (e.g. top buyers, inactive 90 days, by city, by product bought).
- Import/export customer lists; duplicate detection by mobile/email.
- Customers registered on the eCommerce website appear here automatically.
- Opt-in / opt-out flag for marketing messages.

### 4.12 Expense Management
- **Labour cost:** temporary staff (paid per day or per hour) are managed in 4.19; their daily and monthly cost feeds production cost (RMC) and expense reports.
- **Electricity expense:** monthly bill entry (units, amount, dates), meter readings, allocation to production/overhead per unit.
- **Marketing expense:** ads, printing, sampling, influencer, exhibition promotion; campaign-wise entry with date, amount, notes and bill attachment.
- **Rent:** monthly rent entry (recurring) with due date and payment status.
- **Miscellaneous expenses:** every entry needs a description of what it was for, so it can be identified later, plus category, amount, date and bill upload.
- **Other expenses:** transport, repairs, packaging labour and similar; custom categories.
- **Salaries** come from Payroll (see 4.19) and are posted as an expense automatically.
- Each expense is marked as production overhead (added to batch cost, see 4.18) or general overhead.
- Recurring expenses (monthly rent, electricity) with reminders.
- Expense payment mode and receipts upload.
- Expense reports by category, period and product allocation.

### 4.13 Marketing and Messaging
- **New product launch message:** compose a message with image/link and send to selected customers.
- **Occasional product offer message:** festival/seasonal/discount offers to selected segments.
- Channels: WhatsApp, SMS and email. The Company Admin switches each channel on or off in Master Configuration, and a channel becomes active only after the Admin adds that provider's keys (see 4.16).
- Message templates with placeholders (name, product, offer, validity).
- Audience selection: all, group, segment, tag, city, purchase history.
- Schedule sending; send test message; message history and delivery status.
- Respect customer opt-out; daily send limits.
- Offer/coupon management: discount %, flat amount, validity, minimum order, product/category-specific; codes usable on eCommerce site and in the sales bill.
- Birthday/anniversary greetings **[Release 2]**.

### 4.14 Exhibition Management
- Create exhibition: name, venue, city, dates, stall number, notes.
- Exhibition costs: stall fee, travel, stay, staff, decoration, transport, other; total exhibition expense.
- Assign staff to an exhibition.
- **Exhibition stock:** issue stock to exhibition (batch-wise), track units sold, returned and remaining; stock reconciliation on close.
- **Exhibition sales:** quick billing screen for stall (fast, touch-friendly, works with barcode), payment modes, customer capture (name, mobile) for leads.
- Day-wise exhibition sales and expenses.
- Exhibition summary: total sales, cost, profit, ROI, best-selling products, new customers gained.
- **Bulk import of exhibition sales from Excel** (same template, preview and validation flow as 4.10), so stall sales can be entered through the website after the event. Offline billing is not required.
- Compare exhibitions against each other.

### 4.15 Day-Wise Sales Data
- Daily sales register: bills, items, quantity, amount, tax, discount, payment mode split.
- Filter by date range, product, category, customer, staff, channel (counter, online, exhibition).
- Day closing summary: sales, expenses, cash in hand, and difference **[Release 2]**.
- Compare day, week and month.
- Export to Excel/PDF.

### 4.16 Company Settings and Master Configuration (Company Admin)
- Company profile, logo, tax details, bank details, invoice templates and numbering.
- Staff management: create, edit, deactivate; permissions.
- Stock rules: FEFO is fixed, negative stock is not allowed; RMC price basis (latest / average / batch actual).
- Alert thresholds and notification preferences.
- **Master Configuration table** (Company Admin only; each item has an on/off toggle and key fields):
    - Messaging channels: WhatsApp, SMS, email. Toggle each and enter provider keys to activate.
    - Payments: Razorpay keys for the eCommerce site; Cash on Delivery on/off.
    - Custom domain for the company's website.
    - Production/RMC module on/off.
    - Default company tax rates (CGST, SGST, IGST) and CA contact details with the monthly CA sending on/off (see 4.17).
    - Include staff salary in the CA pack: tick or untick (see 4.17).
    - Payroll module on/off (see 4.19).
    - eCommerce website settings (see Section 5.7).
- Keys are stored encrypted and shown masked; a feature stays inactive until valid keys are saved.
- Subscription view: current plan, usage vs limits, renewal date, invoices.
- Data backup export and data import.

### 4.17 GST/Tax Setup and Monthly CA Filing Pack

**Tax setup (company default, product override)**
- **Company-level default tax:** the Company Admin sets the default CGST, SGST and IGST rates once (for example 6% CGST + 6% SGST, with IGST 12%).
- **Product-level tax:** when a product is added, CGST, SGST and IGST are pre-filled with the company default. The user can change them for that product (for example 2.5% + 2.5% or 9% + 9%). HSN code is set per product.
- Tax type per product: taxable, nil-rated, exempt or zero-rated.
- Changing the company default updates only products still on the default; products with their own rates are left as they are. Option to apply a new default to selected products.
- Bills store the tax rate used at the time of billing, so later rate changes never alter old invoices.
- Prices entered as tax-inclusive or tax-exclusive, set per company **[Release 1]**.
- Bulk update of product tax rates through Excel import.
- Audit log of every tax rate change (who, when, old and new value).
- Sales and purchase bills use per-product tax: CGST + SGST for same-state, IGST for inter-state.

**CA contact details**
- Company Admin adds CA name, firm name, mobile and one or more email addresses (with optional CC).
- Toggle to switch the monthly CA popup and sending on or off.
- CA read-only login to view the month's invoices and reports **[Release 2]**.

**Invoice types: B2B, B2C, Export**
- Every sales invoice carries a type that is saved on the invoice: **B2B** (buyer has a GSTIN) or **B2C** (no GSTIN). **Export** (buyer outside India) is a future expansion (###); the type list is built so it can be switched on later.
- The type is suggested from the buyer's GSTIN and can be changed before saving. Online orders are B2C unless the customer enters a GSTIN at checkout.
- (###) When Export is switched on later, export invoices will also hold: country, currency and exchange rate, shipping bill number and date, port code, and whether tax is nil under a Letter of Undertaking (LUT) or IGST is paid.
- Credit and debit notes inherit the type of the original invoice.
- Tax is calculated and totalled separately for B2B and B2C (and for Export later (###)), both in reports and in the CA pack.

**Monthly CA review and send**
1. **Popup:** on the 1st of each month, when the Company Admin opens the dashboard, a popup says "Send last month's GST and tax invoices to your CA". It appears on each dashboard visit until the month is sent, with a "Remind me later" option.
2. **Send to CA** opens a listing of the previous month's financial records, grouped in tabs:
    - Sales invoices: B2B, B2C and credit notes (an Export tab is added later (###)).
    - Purchase bills (raw material, packing, labels, finished goods) with input GST. Raw material cost is included here.
    - Rent invoices or receipts (if available).
    - Electricity, marketing, exhibition, transport and misc expenses, with their bills.
    - Staff salary for the month (payroll register or manual salary expense). This tab appears only when "Include staff salary in the CA pack" is ticked in Master Configuration, and the Admin can untick it for one month at send time.
3. **Listing screen:** each row has a checkbox (with select all per tab, and all tabs), date, number, party, type, taxable value, CGST, SGST, IGST, total, attachment status and verification status. All rows are ticked by default and the Admin unticks what should not go. Filters and search by type, party, amount and date. Live totals of the ticked rows.
4. **Verification:** the Admin can open any row to check it, fix it (edits are logged) and mark it verified. Warnings are shown for problems such as a B2B invoice without a buyer GSTIN, a missing bill attachment or a tax mismatch.
5. **Send (manual):** nothing is emailed automatically. The Admin clicks Send Email, previews the email and pack, and it goes to the CA with a copy to the Admin. Only ticked rows are shared. If any rows are unticked, a confirmation popup lists them and asks "Are you sure?". Normally all rows are sent; unticking is only for rows the Admin still needs to correct, such as a price or a missing calculation.
6. **Pack contents:**
    - Invoice and bill PDFs with their attachments.
    - Excel register per group: invoice number, date, party, GSTIN, type, taxable value, CGST, SGST, IGST, total.
    - **Ledger-based GST calculation:** output GST on sales, shown separately for B2B and B2C (Export later (###)), minus input tax credit on purchases and adjustments for returns, giving net GST payable or refundable split into CGST, SGST and IGST.
    - Rate-wise and HSN-wise tax summary, expense summary, salary summary (only when salary sharing is on) and a list of cancelled invoices. Individual salary slips are included only if the Admin ticks them, and bank details are left out.
7. **After sending:** sent rows are marked "Sent to CA" with date and pack number. Unticked rows stay "Pending" and can go in a later supplementary pack. A record edited after sending is flagged as changed. The Admin can send again or download the pack for any past month.
8. The email goes through the company's email channel in Master Configuration. Failed delivery is retried and alerts the Admin; large packs go as a secure download link that expires after some days.
9. Month lock after sending, so earlier bills change only through credit or debit notes **[Release 2]**.

### 4.18 Production Batches, Quality Check and Batch Pricing

**Terms:** an **inventory lot** is raw material received or entered as opening stock, with its own quantity, price and expiry date (for example 1000 kg). A **batch** is one production run made from one lot, with its own batch number, manufacturing date, expiry date, output, cost and selling price. The raw material lot and the batch each have their own expiry date.

**Flow:** Raw material lot → Batch created → QA In Progress → QA Passed (to Packing), QA Failed (Discard) or Rework (back to QA In Progress) → Batch-wise priced stock → Website and bills.

1. **Opening raw material:** the company starts with raw material lots (quantity, price, supplier, expiry). One lot can produce many batches.
2. **Batch creation:** choose product, lot and raw material quantity used; the quantity is deducted from the lot. **A batch draws from one lot only.** The next lot is used only after the earlier lot is fully used (oldest expiry first), so every batch has one clear expiry and price basis. If the lot has less left than planned, the last batch is simply smaller. Lots are never mixed in one batch, because mixing older and newer material would change the expiry date.
3. **Output and loss:** enter the actual output. The system shows loss quantity and loss % (100 kg in, 95 kg out = 5% loss), with an alert if loss exceeds a threshold set per product. Batch expiry is entered by the user (default from product shelf life), with a warning if it is later than the lot's expiry.
4. **Quality Assurance (QA):** a batch is always in one of four states: **QA In Progress**, **QA Passed**, **QA Failed** or **Rework**. Rework sends the batch back to QA In Progress, and the final result is then QA Passed or QA Failed. Every batch gets a QA report: date, checked by, parameters (custom per product, such as taste, colour, moisture, weight, appearance) with result and remarks, overall Pass/Fail, and attachments (lab report, photos). A batch cannot be packed or sold until QA passes.
    - **Fail:** the batch is discarded with a reason. Its raw material cost is booked as a loss in profit reports.
    - **Pass:** the batch goes to packing.
    - **Rework:** the batch is reworked (reason, actions taken, extra material and labour cost added to the batch cost, extra loss recorded) and returns to QA In Progress. The number of reworks is recorded.
5. **Packing:** the passed batch is packed into sellable units (pack size and count). Packing and label stock is deducted here, and packing loss is recorded. Packed units become sellable stock under that batch. Every pack label carries the batch number, manufacturing date and expiry date printed from the system, and each pack is traceable to its batch.
6. **Batch costing:** batch cost = raw material at lot price + packing + labels + labour + share of production overhead (electricity, rent, salaries, misc). Cost per unit and margin are shown for every batch. **Daily figures are approximate:** overhead is estimated from the month's recurring amounts spread per day. **Month-end costing:** after the month closes, the Admin runs "Finalise month costing", which spreads the actual rent, electricity, salaries and misc across that month's batches and updates batch cost and profit. Reports show Approximate until the month is finalised and Final afterwards.
7. **Batch-wise pricing:** each batch has its own selling price and MRP (defaulting from the product, editable at packing). Sales bills and exhibition issues use batches oldest-expiry first.
8. **Website roll-out:** the website shows the price of the batch currently on sale. When that batch sells out, the next batch goes live with its new price and new expiry date. An order takes only what remains of the current batch. Admin can pause a batch from the website **[Release 1]**.
9. **Batch status:** Created, QA In Progress, Rework, QA Passed, QA Failed (then Discarded), Packing, Ready for sale, Sold out.

*Example:* Lot of 1000 kg. Batch 1 uses 100 kg and yields 95 kg (5% loss); QC fails, so it is discarded. Batch 2 uses 50 kg and yields 47 kg (6% loss); QC passes, so it goes to packing. The lot has 850 kg left for later batches.

### 4.19 Staff, Salary and Payroll
- **Payroll on/off:** if salary is handled by the CA or outside the platform, the Company Admin switches Payroll off in Master Configuration and enters the monthly salary total as an expense instead. Salary still shows in profit reports.
- **Two staff types:** **Permanent** staff are paid monthly (fixed salary); **Temporary** staff are paid per day or per hour. Both can be in the same company.
- Staff profile: name, designation, staff type, joining date, pay basis (monthly, per day, per hour), pay rate, allowances, deductions and statutory details (PAN, PF/UAN, ESI number, state for professional tax). A staff member may or may not have a login.
- Daily attendance (present, half-day, absent, leave, overtime) with monthly summary; hours in and out for hourly staff.
- Monthly payroll run by the Company Admin: salary from attendance, plus allowances, bonus and overtime, minus advances and deductions; approve, then mark paid with date and payment mode.
- **Statutory deductions (#):** PF, ESI, Professional Tax and TDS on salary are calculated automatically and shown on the slip, with employer contributions tracked separately. Each staff member has on/off flags for PF and ESI. Rates, wage limits and slabs (Professional Tax is state-wise) live in a configurable statutory master so they can be updated when the law changes. TDS uses the tax regime and declarations the staff member provides. Monthly PF, ESI, PT and TDS statements are available for the CA. Filing and paying them on government portals is planned for Release 3.
- **Salary slip** per staff per month (PDF) with earnings, deductions, net pay and attendance. Staff see and download only their own slips; the Admin sees all.
- **Bank details:** staff add and update their own (account holder, account number, IFSC, bank, branch, UPI). Details are checked through a third-party bank verification API (IFSC and account details) and can be saved only after the check passes, so no Admin approval is needed. Numbers are masked and every change is logged.
- Salaries post automatically as an expense and feed batch cost and profit reports.
- Advance and loan tracking with a deduction schedule **[Release 2]**.
- Payroll reports: salary register and month-wise payout.

### 4.20 Inventory Control Enhancements
Found in leading inventory software (Zoho Inventory, Odoo, Fishbowl) and not yet covered above.
- **Physical stock count:** full and cycle counts by category, location or batch; enter or scan counted quantity; variance report; stock is adjusted only after Admin approval.
- **Write-off types:** expired, damaged, sample, gift, own use, QC-rejected; each with a reason and booked to the right expense.
- **Approval rules:** adjustments and write-offs above a set value need Company Admin approval; bulk adjustments through Excel.
- **Purchase order and goods receipt (GRN):** receive goods against a PO, partial receipts, ordered vs received vs billed comparison, supplier returns. Low-stock alerts convert to draft POs in one click.
- **Incoming raw material QC:** each raw material lot is accepted or rejected on receipt, with remarks, before it becomes usable stock **[Release 2]**.
- **Batch recall:** mark a batch as recalled; it is blocked from sale and from the website, the customers and bills that received it are listed, and they can be notified by message.
- **Barcode scanning** (phone camera or USB scanner) in billing, exhibition billing, stock count and goods receipt.
- **Combo/bundle products** (gift packs made of several products; stock deducted from the parts) **[Release 2]**.
- **Customer-group price lists** (retail, wholesale, distributor) applied automatically on billing **[Release 2]**.
- **Multiple locations** (factory, shop, stall) with stock transfers, in-transit status and bin/rack labels **[Release 2]**.
- **Cash book, bank book and day book** with cheque tracking **[Release 2]**.

### 4.21 Product Compliance and GST Rules (India) **[Compliance]** **[Release 1]**
**Legal Metrology (packaged goods)**
- Fields per product and pack: manufacturer/packer/importer name and address, generic name, net quantity, MRP inclusive of all taxes, consumer care details, country of origin (imported goods), dimensions where relevant, date of manufacture or packing, best before or expiry date (taken from the batch).
- MRP is stored per batch (see 4.18) and always tax-inclusive; a selling price above MRP is blocked.
- Pack labels can be printed with these fields.

**FSSAI (applies to categories with the Food compliance profile)**
- Company FSSAI licence number; per product: veg/non-veg symbol, ingredients, nutrition information per 100 g/ml, allergen information, storage and usage instructions, batch/lot number on the label.
- Shown on the product page and label template.

**GST rules**
- **HSN is required on every product:** it is a mandatory field when a product is added and in Excel imports, and it is printed on all GST invoices, including B2B and export bills. Minimum 4 digits. From ₹5 crore turnover, 6 digits are required: at ₹4.5 crore the Admin gets a popup to prepare the 6-digit codes, and at ₹5 crore a product without a 6-digit HSN cannot be billed. Because every product already has HSN, activating Export (a future expansion (###)) needs no separate HSN step.
- **Turnover tracker (follows the GST "aggregate turnover" definition):** the financial year's sales across all channels, including taxable, exempt and export sales, without GST and cess. The Admin can add turnover brought forward from earlier years. Each company has one GSTIN and one PAN, so no other registrations are combined. At ₹4.5 crore the Admin gets a popup to prepare 6-digit HSN codes. On crossing ₹5 crore, a second popup explains that B2B and export e-invoicing (IRN) generally starts from the next financial year and stays applicable even if turnover later falls; B2C invoices are outside e-invoicing.
- **e-Invoicing applicable** setting with an "applicable from" date, as in Tally. Once set, the e-invoice fields are used on B2B invoices; the IRN module itself is Release 2 (see below).
- GSTIN format check for company, customers and suppliers; state code and place of supply derived automatically.
- Bill of Supply for composition-scheme or exempt sales; reverse-charge flag on purchase bills. **[Release 2]**
- Invoice numbers are consecutive, unique per financial year, and no longer than 16 characters.
- **Delivery challan** for stock sent to exhibitions or on approval without a sale; the invoice follows when a sale happens.
- **e-Invoice (IRN and QR code)** is mandatory for B2B invoices once a company's turnover reaches ₹5 crore. Not in the first release, but invoice fields (IRN, acknowledgement number, QR, transporter and vehicle details for e-way bill) are reserved so it can be added as an optional module **[Release 2]**.
- CA pack tables follow GSTR-1 sections: B2B, B2C, credit/debit notes, HSN summary, documents issued (an export table comes with Export (###)).

---

## 5. eCommerce Website (Per Company)

All companies use one common storefront design (no custom design per company). The website and its APIs are enabled only for companies on the Inventory Panel + eCommerce Website plan. Each company gets its own website name and custom domain, which the Company Admin manages from Master Configuration in the common Admin Panel. The storefront talks to the platform through APIs scoped to one company (via its domain and API key), so a website can only ever access its own company's products, customers and orders.

### 5.1 Customer Registration and Login
- Register with name, mobile, email, password.
- Mobile/email OTP verification.
- Login with email/mobile + password or OTP.
- Social login **[Release 2]**.
- Forgot/reset password, change password.
- Profile management.
- Customer account is created in that company's customer master.
- Guest checkout **[Release 1]**.

### 5.2 Product Listing
- Grid/list view with images, price, MRP, discount badge, stock status.
- Category and sub-category navigation.
- Search with suggestions and filters (category, price range, brand, availability).
- Sorting (price, newest, popularity).
- Pagination or infinite scroll.
- Only products marked "visible" are shown. Products with zero stock stay listed but show "Currently out of stock" and cannot be added to the cart.
- The price shown is that of the batch currently on sale; when it sells out, the next batch goes live at its own price (see 4.18).

### 5.3 Product Detail Page
- Image gallery with zoom, description, price, MRP, tax info, unit/pack size.
- Real-time stock availability; quantity selector limited to available stock; "Currently out of stock" message when none is left.
- Variants, ingredients/specs, usage instructions, and the mandatory declarations listed in 4.21 and 5.10.
- Add to cart and buy now.
- Add to wishlist **[Release 2]**.
- Related products; customer ratings and reviews (see 5.13).
- Share product link; SEO-friendly URL and meta tags.

### 5.4 Cart and Checkout
- Cart with quantity update, remove, price summary, tax and shipping calculation.
- Apply coupon/offer code.
- Address selection at checkout; delivery method (home delivery / pickup); optional GSTIN entry so the order becomes a B2B invoice.
- Payment: online through **Razorpay** (cards, UPI, netbanking, wallets) and Cash on Delivery; the Company Admin can switch each on or off in Master Configuration.
- Order review and confirmation page; confirmation email/SMS/WhatsApp.
- Stock re-check at the moment of order placement.

### 5.5 Order Management (Customer Side)
- My Orders list with status and filter.
- Order detail: items, amounts, address, payment, status timeline.
- Track order; download invoice.
- Cancel order (before dispatch), request return/refund **[Release 1]**.
- Reorder previous order.

### 5.6 Address Management
- Add, edit, delete addresses; set default; label (home, office).
- Separate billing and shipping addresses.
- Pincode serviceability check.

### 5.7 Store Content and Settings (Managed by Company Admin)
- Store branding within the common design: website name, logo, colours, banner images, home page sections (featured, new arrivals, best sellers).
- Static pages: About and Contact. Terms, Privacy, Shipping/Return policy and FAQs are managed as described in 5.12.
- Shipping rules: flat rate, free above amount, by pincode/zone.
- Payment method settings (Razorpay keys, COD on/off), see 4.16.
- Custom domain mapping, entered by the Company Admin in Master Configuration.
- SEO settings, social links, contact form, WhatsApp chat button.
- Website on/off switch; maintenance mode.

### 5.8 Backend Order API (Key Requirement)
The API accepts an order from the company's website and creates it in the platform **after validating products and stock**.

- Company-scoped authentication (per-company API key) plus customer token.
- Product and category list, product detail and live stock availability APIs.
- Customer register, login and profile APIs.
- Address CRUD APIs.
- Cart validation API (price, tax, stock, coupon).
- **Create order API:** validates that each product exists, is active and has enough stock (negative stock is not allowed); re-calculates prices server-side (client prices are never trusted); reserves/deducts stock; rejects with a clear error listing which items failed.
- Order list, detail, status and cancel APIs.
- Payment callback/webhook handling.
- Blog, policy, FAQ and feedback APIs (see 5.12 and 5.13).
- Idempotency to prevent duplicate orders on retry.
- Rate limiting, request logging and API versioning.
- Auto-created online order shows in the Admin Panel with status "New" and notifies the Admin/Staff.

### 5.9 Online Order Handling (Admin Side)
- Order inbox with statuses: New, Confirmed, Packed, Shipped, Delivered, Cancelled, Returned.
- Confirm/reject, edit before dispatch, assign to staff.
- Convert order to a sales bill with batch selection; stock deducted accordingly.
- Update status with tracking number and courier name; customer notified on every change.
- Payment status: Pending, Paid, Failed, Refunded; COD collection tracking.
- Refund and return handling; stock added back on return.
- Abandoned cart list **[Release 2]**.

### 5.10 Storefront Compliance and Trust **[Compliance]** **[Release 1]**
Based on the Consumer Protection (E-Commerce) Rules, 2020 and Legal Metrology rules.
- **Business details** on the footer and policy page: legal name, address, GSTIN, FSSAI licence number (food), customer care number and email, grievance officer name and contact.
- **Total price with break-up** (product, tax, shipping, COD charge); no hidden charges at checkout.
- **Product page declarations:** net quantity, MRP, expiry or best-before date, country of origin, manufacturer details, ingredients and nutrition (food).
- Return, refund, exchange, warranty, delivery and payment information visible to the customer.
- **Explicit consent:** no pre-ticked boxes for terms or marketing.
- **Complaints:** customer raises a complaint from the account or contact page and gets a ticket number and status tracking. Acknowledged within 48 hours and resolved within one month, with SLA timers and overdue alerts for the Company Admin.
- Cancellation charges follow the rules; the default is none.

### 5.11 Additional Storefront Features (Market Comparison)
- **Stock reservation** at checkout with a timeout (for example 15 minutes), so unpaid online orders release stock.
- **Returns:** return window and reasons, approval, refund to original payment or store credit, and stock re-entry or write-off depending on condition.
- **Razorpay handling:** full and partial refunds from the Admin Panel, payment status through webhooks with signature check, retry on failed payment, daily settlement reconciliation report.
- **Shipping:** courier name and tracking number entered manually now; optional automated courier integration (rates, pincode serviceability, labels, tracking updates) as a Release 2 module **[Release 2]**.
- **COD controls:** COD charge, order value limit, pincode-wise availability, and OTP/WhatsApp confirmation before dispatch to reduce returns **[Release 1]**.
- "Notify me when back in stock" for out-of-stock products **[Release 2]**.
- Abandoned cart reminders by email or WhatsApp **[Release 2]**.
- SEO basics: sitemap, structured product data, meta tags, clean URLs, fast loading.
- Google Analytics and Meta Pixel IDs in Master Configuration **[Release 1]**.
- Security: CAPTCHA on registration and login, rate limiting, no card data stored (Razorpay handles payment details).
- **Webhooks** for order and stock changes sent to the storefront, plus API documentation and a test key per company.

### 5.12 Website Content: Blogs, Policies and FAQs (Company Admin)
**Blogs**
- Company Admin creates, edits, schedules, publishes, unpublishes and deletes blog posts in the Admin Panel; they appear on that company's website only.
- Fields: title, URL slug, cover image, rich-text body with images, category and tags, author, publish date, SEO title and description, optional related products.
- Status: draft, scheduled, published, archived.
- Website: blog list with categories, blog detail page, share buttons and related posts.
- Comments on posts, with moderation **[Release 2]**.

**Policies and documents**
- Company Admin adds and edits Terms and Conditions, Privacy Policy, Shipping policy and Return/Refund policy, as rich text or an uploaded PDF.
- Each policy keeps versions with a published date. The version a customer accepted is stored with their consent record (see 7.1). When a new Terms or Privacy version is published, customers must accept it at their next login or checkout.
- Shown in the website footer and linked at registration and checkout.
- Super Admin can supply default policy templates for companies to start from **[Release 2]**.

**FAQs and documents**
- FAQ groups (for example Orders, Payment, Delivery, Returns) with questions and answers, ordering, show/hide per item, and search on the website.
- Downloadable documents (for example catalogue or product care guide) shown on a Downloads page.

### 5.13 Customer Feedback and Reviews
- Customers can give: product reviews (star rating, text, photos) after delivery, order and delivery feedback, and general feedback or suggestions from a Feedback page. Complaints stay separate tickets (see 5.10).
- Only verified buyers can review a product. Each review is linked to the order and the batch, so quality problems can be traced.
- Feedback inbox for the Company Admin and Staff: filter by type, rating and product; reply; mark resolved; publish or hide reviews (moderation); assign to a staff member.
- Alert to the Admin for low ratings (default 2 stars or below, configurable).
- Optional feedback request message after delivery by email or WhatsApp, switched on by the Company Admin (off by default).
- Reports: average rating by product and batch, feedback volume, low-rated items.

### 5.14 Customer Mobile App (Flutter) **[Release 2]**
- A Flutter app (Android and iOS) for the company's customers, with the same features as the storefront: catalogue, product page with declarations, cart and checkout (Razorpay and COD), account, orders, addresses, feedback and complaints.
- Uses the same company-scoped storefront APIs as the website (5.8); no separate backend.
- Details (one app per company or one shared app, store publishing, push notifications) will be agreed before Release 2 starts; the developer will provide boilerplate code.

---

## 6. Reports

Every report supports date range, filters, on-screen view, and export to Excel/PDF. Company Admin can control which staff see which reports.

### 6.1 Stock Reports
- Current stock summary: finished goods, raw material, packing, labels.
- Stock valuation report (cost and selling value).
- Batch-wise stock and expiry report; near-expiry and expired stock.
- Low-stock / reorder report.
- Stock movement/ledger per item.
- Dead and slow-moving stock; fast-moving stock.
- Stock ageing.

### 6.2 Sales Reports
- Day-wise, week-wise, month-wise, year-wise sales.
- Product-wise, category-wise, customer-wise, staff-wise sales.
- Channel-wise: counter, online, exhibition.
- Invoice-type wise: B2B and B2C sales (Export later (###)), each with separate tax totals.
- Financial-year turnover against the ₹4.5 crore alert and the ₹5 crore limit.
- Payment mode report; discount report; tax (GST) summary; monthly GST ledger (output tax, input tax credit, net payable; see 4.17).
- Sales returns report.
- Top and bottom products; top customers.
- Receivables and customer outstanding ageing.

### 6.3 Purchase Reports
- Purchase register; supplier-wise, item-wise purchases.
- Raw material price trend and price comparison across suppliers.
- Payables and supplier outstanding ageing.
- Purchase returns.

### 6.4 Cost and Profit Reports
- **Product RMC report** and total cost per unit breakdown.
- Product-wise margin and profitability.
- Batch-wise profit.
- Profit and Loss (period-wise): sales – purchases/COGS – expenses.
- Expense report by category (labour, electricity, marketing, others).
- Labour cost report (daily/monthly).
- Cash flow summary: money in vs money out **[Release 2]**.
- Break-even indicator per product **[Release 2]**.

### 6.5 Production Reports
- Production log; raw material consumption; yield vs wastage.
- Packing and label consumption.

### 6.6 Customer and Marketing Reports
- New vs repeat customers; customer lifetime value.
- Inactive customers (win-back list).
- Message campaigns: sent, delivered, failed; sales after campaign.
- Marketing spend vs sales generated.
- Offer/coupon usage.

### 6.7 Exhibition Reports
- Exhibition-wise sales, expenses, profit and ROI.
- Day-wise exhibition sales; product performance per exhibition.
- Stock issued vs sold vs returned; leads captured.
- Exhibition comparison.

### 6.8 Online Store Reports
- Orders by status; conversion and cancellation rates.
- Feedback and ratings: average rating by product and batch, low-rated items (see 5.13).
- Best-selling online products; sales by city/pincode.
- Abandoned carts **[Release 2]**.

### 6.9 Owner Insight Reports (Best Overview for the Admin)
- **Business health dashboard:** revenue, cost, profit, cash position, stock value at a glance.
- **Reorder suggestions:** what to buy and how much, based on sales speed.
- **Profit leakage report:** products sold below cost, high wastage, expiring stock value.
- **Best exhibition and channel report:** where the most profit comes from.
- Month-over-month and year-over-year comparison.
- Scheduled reports emailed to the Admin (daily/weekly/monthly).

### 6.10 Batch and Period Profit Analytics
The Company Admin can see complete profit, with charts, tables and drill-down, for:
- **Each batch:** revenue minus batch cost (raw material, packing, labels, labour, allocated overhead) = profit and margin %, with units sold vs remaining. Discarded batches show as a loss.
- **Each inventory lot:** all batches from the lot, raw material cost, output, loss %, QC pass rate, revenue and profit.
- **Each day, week, month, quarter and year:** sales revenue (excluding tax) minus cost of units sold, minus period expenses not already in batch cost (rent, electricity, salaries, marketing, misc), minus discarded batch losses = net profit. Quarters follow the company's financial-year start.
- Drill down from year to quarter, month, week, day, then to bills and batches; compare any two periods.
- Filters by product, batch, lot and channel; export to Excel/PDF.
- Value of unsold stock is shown separately so profit is not misread.
- **Overall company profit:** total earnings minus total amount invested in the period (purchases, production costs, expenses, salaries), shown next to the batch-based profit. Amounts exclude GST.

---

## 7. General Platform Features

- **Notifications:** in-app, email, optional SMS/WhatsApp for low stock, expiry, new orders, payment due, subscription expiry.
- **Global search** across products, customers, bills.
- **Data import/export:** Excel/CSV for products, customers, stock, suppliers, opening balances, orders and sales bills.
- **Attachments:** upload bills, images, documents.
- **Tax and currency setup per company:** India GST and INR now; database and tax logic are designed so other countries' tax systems can be added later (#). Multi-language UI **[Release 2]**.
- **Responsive UI** that works on desktop, tablet and mobile.
- **Print support:** A4, thermal receipt, barcode labels.
- **Audit trail** for stock, bills and price changes.
- **Backups and restore**; company data export on request.
- **Security:** encrypted passwords, HTTPS, tenant data isolation, role-based permissions, API keys per company, optional two-factor authentication **[Release 2]**.
- **Help and onboarding:** setup checklist for new companies, sample data.

### 7.1 Privacy and Data Protection (India DPDP Act and Rules) **[Compliance]** **[Release 1]** (consent notice and records); rights, retention and breach items are Release 2, before May 2027
- Standalone privacy notice at registration and checkout: what data is collected, why, and how to withdraw consent or complain.
- Consent records (who, what, when, notice version); marketing opt-in per channel; withdrawing consent is as easy as giving it.
- Customer rights on the account page: view, correct, download and request deletion of their data; Admin handles erasure requests with a log. **[Release 2]**
- Retention rules: personal data kept only as long as needed (tax records as the law requires), with notice before erasure. **[Release 2]**
- Personal data breach log and alert workflow, ready for the 72-hour report to the authority. **[Release 2]**
- Sensitive data (bank details, API keys) encrypted and masked; access logs for who viewed it.
- Staff data (bank details, salary) treated as personal data with restricted access.
- Age declaration at registration; block or parental consent for under 18 **[Release 2]**.
- Core duties apply from about 13 May 2027. Each company is the data owner and the platform processes data for it (agreement covered in the Technical Document).

---

## 8. Out of Scope for This Version (Proposed)

- Accounting/general ledger with full double-entry books.
- Filing and paying PF, ESI, professional tax and TDS on government portals: planned for Release 3. In Releases 1 and 2 payroll calculates them and produces statements (see 4.19).
- Native mobile apps in Release 1 (web is responsive). A Flutter customer app for the eCommerce store is planned for Release 2 (see 5.14).
- Automated courier integration and shipping labels (manual courier and tracking entry is in scope; automation is an optional Release 2 module, see 5.11).
- Government e-invoice (IRN) and e-way bill API integration in the first release (fields are reserved, optional Release 2 module; see 4.21).
- Tax systems of other countries: not built now, only kept possible by design (#).
- Export sales and export invoices: future expansion (###).
- Direct filing of GST returns (GSTR-1, GSTR-3B) on the government portal: planned for Release 3. Until then the CA receives the data and files it.
- Multi-branch stock transfer between companies.

Tell me if any of these should be moved into scope.

---

## 9. Decisions Recorded

| # | Topic | Decision |
|---|---|---|
| 1 | Data access | Super Admin has full access and can manage everything, including each company's business data. |
| 2 | Permissions | Configurable at two levels: Super Admin configures Company Admin roles and access; Company Admin configures Staff roles and access. |
| 3 | Messaging | WhatsApp, SMS and email are all supported. Company Admin toggles each and adds keys in Master Configuration. |
| 4 | Payments | Razorpay. Cash on Delivery is configurable by the Company Admin. |
| 5 | Tax | GST invoicing and India tax now; database design stays scalable for other countries (#). |
| 6 | Storefront | One common design, no per-company custom design. We maintain each company's website name; each website accesses only its own company's products. |
| 7 | Domains | Each company has its own custom domain, entered by the Company Admin in Master Configuration. |
| 8 | Stock rule | FEFO. Negative stock not allowed. Out-of-stock products show "Currently out of stock" on the website. |
| 9 | Exhibition billing | No offline mode. Company Admin works through the website, with bulk Excel import for orders and sales. |
| 10 | Scale | About 10 companies, 50 to 60 products per company. |
| 11 | Production | Switchable per company. |
| 12 | GST setup | Company-level default CGST/SGST/IGST, pre-filled on each new product and editable per product. |
| 13 | CA monthly invoices | On the 1st of each month the Company Admin sees a dashboard popup, reviews and selects the month's invoices and financial records, and sends them to the CA. Sales are tagged B2B or B2C. |
| 14 | Production flow | Raw material lot → batch (one lot per batch) → QC → packing → batch-wise priced stock; see 4.18. |
| 15 | Payroll | Salary roll-out, salary slips and staff bank details are in scope; see 4.19. |
| 16 | Sending to CA | Always manual. The popup appears on the 1st, the Company Admin clicks Send Email. No email goes out automatically. Unticked items need an "Are you sure?" confirmation. |
| 17 | Salary in CA pack | Configurable checkbox per company: salary shared with the CA as an expense, or not. Payroll itself can be switched off. |
| 18 | Export | Future expansion, not built now (###). |
| 19 | Categories | Super Admin adds global categories, each Company Admin adds own; compliance fields depend on the category. |
| 20 | HSN | Required on every product (minimum 4 digits) and shown on all GST invoices, including B2B and export. 6 digits required from ₹5 crore turnover, with a popup at ₹4.5 crore. |
| 21 | Salary as expense | With Payroll off, the Admin enters a monthly salary total as an expense. |
| 22 | Website content | Company Admin manages blogs, Terms and Conditions, Privacy Policy, FAQs and documents; customers can give feedback and reviews. |
| 23 | Suggested features | All accepted as requirements. Release 1 or Release 2 for each is listed in Section 13 and confirmed. |
| 24 | Subscription plans | Two plan types: Inventory Panel only, and Inventory Panel + eCommerce Website, each with weekly, monthly and yearly plans. |
| 25 | Razorpay | The Super Admin's own Razorpay collects subscription fees; each Company Admin uses their own Razorpay for the store. |
| 26 | Lots and batches | A batch uses one lot only; the last batch may be smaller; lots are never mixed. |
| 27 | Packing and labels | Pack labels carry batch number and expiry date, tracked in the system. |
| 28 | Costing | Daily figures are approximate; a month-end costing run finalises batch cost and profit. |
| 29 | Website batches | When a batch sells out, the next batch goes live with its new price and expiry date. |
| 30 | QA states | QA In Progress, QA Passed, QA Failed, Rework (then back to QA In Progress). |
| 31 | Staff and payroll | Permanent (monthly) and Temporary (per day or per hour) staff; PF, ESI, Professional Tax and TDS calculated; portal filing not included. |
| 32 | Bank details | Verified through a third-party API; no Admin approval needed. |
| 33 | Profit | Excludes GST. Overall profit = total earnings minus total amount invested, shown with batch-based profit. |
| 34 | HSN and Export | Covered by row 20: HSN is always required, so Export activation needs no separate HSN step. |
| 35 | Turnover | GST aggregate turnover, with alerts at ₹4.5 crore and ₹5 crore and an "e-Invoicing applicable" setting. |
| 36 | Policy versions | Customers accept a new Terms or Privacy version at their next login or checkout. |
| 37 | e-Invoice | First release has the GST tax invoice only; e-invoice fields are reserved. |
| 38 | Company identity | One GSTIN and one PAN per company. Another GSTIN or PAN needs a new company. |
| 39 | Portal filing | Filing and payment on government portals (GST returns, PF, ESI, Professional Tax, TDS) is outside Releases 1 and 2 and planned for Release 3. |
| 40 | Technology | Backend and APIs in .NET, Admin Panel and storefront website in React, PostgreSQL database. |
| 41 | Mobile app | A Flutter customer app for the eCommerce store is planned for Release 2 (see 5.14); details are agreed before Release 2 starts. |

---

## 10. Remaining Points to Confirm

None. All points are answered and recorded in Section 9. The document is ready to freeze on your confirmation.

---

## 11. Notes on Markers

**(#) Design note, not a user-facing feature.** India GST is the only tax system delivered now, but the database design and tax logic must stay scalable so other countries' tax systems can be added later without a redesign. This is handled in the Technical Document.

**(###) Future expansion, not built now.** Export sales (export invoices, currencies, LUT or IGST handling, shipping bill details) are planned for later. The first release does not show them, but the invoice type, tax calculation and CA pack are designed so Export can be switched on without a redesign.

---

## 12. Research Notes and Gaps Added

I compared this document with public feature lists and Indian rules. Compliance items are summaries of public sources, so please confirm them with your CA or legal advisor.

| Area checked | What I found | Added in |
|---|---|---|
| Inventory software (Zoho Inventory, Odoo, Fishbowl) | Stock counts, adjustment approvals, purchase orders and receipts, transfers and bin locations, price lists, bundles, barcode scanning, webhooks | 4.20, 5.11 |
| Food and batch tracking software | Batch quality records, expiry and recall traceability | 4.18, 4.20 |
| Indian eCommerce checklists (Shiprocket) | Guest checkout, several payment options, COD verification, refunds, returns and exchange, courier tracking, analytics, security | 5.11 |
| Consumer Protection (E-Commerce) Rules, 2020 | Seller details, grievance officer, complaint timelines, price break-up, no pre-ticked consent | 5.10 |
| Legal Metrology (Packaged Commodities) Rules | Mandatory pack declarations, MRP inclusive of tax, declarations also shown online | 4.21, 5.10 |
| FSSAI Labelling and Display Regulations | Batch number, expiry, veg/non-veg symbol, nutrition, licence number | 4.21 |
| GST rules | HSN digits by turnover, e-invoice at ₹5 crore, e-way bill, delivery challan | 4.21, 8 |
| GST aggregate turnover and Tally | Turnover is counted PAN-wise on all supplies (taxable, exempt, export) without GST; e-invoicing applies from the year after ₹5 crore is crossed; Tally has an "e-Invoicing applicable" setting with a date | 4.21 |
| DPDP Act and Rules 2025 | Consent notice, rights, retention, 72-hour breach report, phased from May 2027 | 7.1 |
| Multi-tenant SaaS practice | Fair-use limits, offboarding, GST invoices for subscriptions, support tickets | 3.2, 3.3 |

**Sources:** zoho.com/inventory; shiprocket.in/blog/top-10-must-have-features-for-an-ecommerce-website; mondaq.com (Consumer Protection E-Commerce Rules); ssrana.in (Legal Metrology); fssai.gov.in (Labelling and Display compendium); tallysolutions.com (HSN in e-invoices); incorpx.io (e-invoice thresholds); jsalaw.com and ey.com (DPDP Rules 2025); busy.in, taxguru.in and tallysolutions.com (aggregate turnover and e-invoice applicability).

---

## 13. Accepted Suggestions and Release Split

You accepted all my suggestions, so each one is a requirement now. Release 1 means the first release and Release 2 means after it. You confirmed this release split.

| Feature | Section | Release | Details |
|---|---|---|---|
| Session management | 2 | Release 1 | Auto-logout after inactivity (default 30 minutes, configurable), "log out from all devices", and a list of active sessions. |
| Wholesale price | 4.3 | Release 1 | A separate wholesale price on each product, used for wholesale customers. |
| Purchase orders with approval | 4.9 | Release 1 | PO with supplier, items and expected date; statuses draft, approved, partly received, closed; Admin approval above a set value. |
| Tax-inclusive or tax-exclusive prices | 4.17 | Release 1 | Per-company setting; bills calculate tax accordingly. |
| Pause a batch on the website | 4.18 | Release 1 | The batch stays in stock but is not sold online; the next batch goes live if there is one. |
| Guest checkout | 5.1 | Release 1 | Order without an account (name, mobile, email, address, mobile OTP), with a prompt to create an account afterwards. |
| Return and refund requests | 5.5, 5.11 | Release 1 | Customer requests a return with a reason and photos; the Admin approves; refund follows 5.11. |
| COD controls | 5.11 | Release 1 | COD charge, minimum and maximum order value, pincode availability, OTP or WhatsApp confirmation before dispatch. |
| Analytics IDs | 5.11 | Release 1 | Fields for Google Analytics and Meta Pixel; loaded on the website only when filled in. |
| Coupons on subscription plans | 3.2 | Release 2 | Code, percentage or flat amount, validity, usage limit, applicable plans. |
| Support tickets to Super Admin | 3.3 | Release 2 | Subject, category, priority, attachments, status, reply thread and notifications. |
| Multiple locations and transfers | 4.2, 4.20 | Release 2 | Stock per location (factory, shop, stall), transfers with in-transit status, bin/rack labels. |
| Product variants | 4.3 | Release 2 | Size, flavour or pack attributes; each variant has its own SKU, barcode, price, stock and batches; selector on the website. |
| Margin alert | 4.6 | Release 2 | Minimum margin % per product; alert when a raw material price change breaks it. |
| Quotations | 4.10 | Release 2 | Quote number, validity date, statuses (draft, sent, accepted, expired), PDF sharing, convert to invoice. |
| Birthday and anniversary greetings | 4.13 | Release 2 | Template per occasion, sent on the day to opted-in customers through the chosen channels. |
| Day closing | 4.15 | Release 2 | Opening cash, sales by payment mode, expenses, expected vs counted cash and the difference; the day is locked after closing. |
| CA read-only login | 2, 4.17 | Release 2 | Login linked to one company to view and download invoices, bills and ledgers only; the Admin can revoke it. |
| Month lock | 4.17 | Release 2 | Lock a month after sending to the CA; later changes only through credit or debit notes. |
| Advance and loan tracking | 4.19 | Release 2 | Amount, instalments and balance; deducted automatically in payroll. |
| Incoming raw material QC | 4.20 | Release 2 | Accept or reject a lot on receipt, with remarks. |
| Combo/bundle products | 4.20 | Release 2 | Gift pack of several products with its own price; stock is deducted from the parts. |
| Customer-group price lists | 4.20 | Release 2 | Retail, wholesale and distributor prices applied by customer group. |
| Cash, bank and day book | 4.20 | Release 2 | Entries created from receipts, payments and expenses; cheque status (issued, deposited, cleared, bounced). |
| Social login | 5.1 | Release 2 | Sign in with Google. |
| Wishlist | 5.3 | Release 2 | Save products and move them to the cart. |
| Abandoned carts | 5.9, 5.11, 6.8 | Release 2 | Cart list, reminder by email or WhatsApp to opted-in customers with a limit on reminders, recovered-order report. |
| Back-in-stock notification | 5.11 | Release 2 | Customer subscribes on an out-of-stock product and gets one message when stock returns. |
| Automated courier integration | 5.11 | Release 2 | Rates, pincode serviceability, labels and tracking updates through a courier partner. |
| Blog comments | 5.12 | Release 2 | Comments are moderated before they appear. |
| Default policy templates | 5.12 | Release 2 | Super Admin provides starter Terms, Privacy and Return policy templates. |
| Cash flow summary and break-even | 6.4 | Release 2 | Money in vs money out per period; units a product must sell to cover its cost. |
| Two-factor authentication | 7 | Release 2 | Authenticator app or email OTP for admins; the Company Admin can require it for staff. |
| Multi-language UI | 7 | Release 2 | English first; Hindi and Gujarati proposed. |
| Age declaration at registration | 7.1 | Release 2 | Tick for 18 years or older; block or parental consent otherwise. |

**Compliance items in Release 2:** Bill of Supply and reverse-charge flag (4.21), the e-Invoice module (4.21; the invoice fields are reserved in Release 1), and customer data rights, retention rules and the breach log under DPDP (7.1), which must be ready before May 2027.

**Release 2 also includes** the Flutter customer app (5.14).

**Release 3 (planned):** filing and payment on government portals for GST returns (GSTR-1, GSTR-3B), PF, ESI, Professional Tax and TDS.
