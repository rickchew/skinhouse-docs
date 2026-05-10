# SKIN HOUSE - Frontend Documentation

**Framework:** CodeIgniter 3.1.10
**App Version:** v1.5.1
**Currency:** RM (Malaysian Ringgit)

---

## Global Layout

- **Header:** Search bar (global), user profile icon (top-right)
- **Sidebar (left):** Fixed navigation with collapsible sections
- **Content area:** Right of sidebar, scrollable
- **Footer:** Render time, CodeIgniter version, app version

---

## Navigation Structure

```
SKIN HOUSE
  |-- Dashboard
  |-- Insight
  |-- Order
  |-- Invoice
  |-- Staff
  |-- Appointment
  |-- Inventory
  |     |-- Stock Summary
  |     |-- Stock Transaction
  |     |-- Inventory Entry
  |     |-- Manage Product
  |     |-- Product Category
  |-- CRM
  |     |-- Members
  |     |-- Push Notification
  |-- Report
  |     |-- Sales Report
  |     |-- Assign Report
  |     |-- PVSV Report
  |     |-- Taken Report
  |     |-- Item Sales Report
  |     |-- Balance Report
  |     |-- Birthday
  |-- Master Control
  |     |-- Users Group
  |     |-- Staff
  |-- Logout
```

---

## Branches (Outlets)

The system manages multiple branches:
- **SUTERA**
- **NAN YANG PLACE**
- **MARINA**
- **PETALING JAYA**

---

## Pages

### 1. Dashboard (`/`)

**Summary cards (top):**
- Today's revenue (RM) with yesterday comparison
- Revenue trend line chart (date-range, filterable by "All Orders")
- Invoice Total / Assigned Total / Taken Total
- New Members count + Total Spending
- Overall Members count + Total Spending

**Recent Orders table:**
| Column | Description |
|--------|-------------|
| # | Order number |
| Datetime | Order date |
| Branch | Branch name + staff name |
| Member | Customer name |
| Package Price | Total package price |
| Total Paid | Amount paid |
| Last Update | Last modification date |
| Actions | "..." menu |

**Actions:** + New Order button

---

### 2. Insight (`/insight/`)

**Tabs:** Overview | Sales | Members | Product
**Filters:** Branch (ALL / specific), Date range picker

#### Overview tab
- **Sales Overview:** Combined bar + line chart (Orders count + Invoice amount by date)
- **Product Hot Sellers:** Stacked bar chart (top 3 products by date)
- **Members' Source by Branch:** Stacked bar chart (Facebook / Instagram / Others per branch)

#### Sales tab
- **Sales Overview:** Same as overview
- **Beautician's Sale:** Bar chart by staff name
- **New Members' Spending:** Combined bar + line chart (Total Spending + New Member count by date)

#### Members tab
- **Members' Source by Branch:** Stacked bar chart
- **Members' Gender:** Donut chart (Male / Female %)
- **Members' Birthday:** Bar chart by date

#### Product tab
- **Product Sales by Category:** Pie chart (Aesthetic Procedure, Treatment, Product, Chiropractic Procedure, Semi Permanent Embroidery)
- **Products Transaction:** Bar chart (Stock In / Stock Out by date)
- **Product Hot Sellers:** Stacked bar chart

---

### 3. Order (`/order/`)

**Filters:** Balance Filter, Branch Filter
**Actions:** + New Order, + New Member

**Order list table:**
| Column | Description |
|--------|-------------|
| # | Order number |
| Date | Order date |
| Branch | Branch + staff |
| Member | Customer name + treatment/product items listed inline |
| Package Price | Total price |
| Total Paid | Amount paid |
| Balance | Outstanding |
| Last Update | Date |
| Status | Badge (COMPLETED) |
| Actions | "..." -> View Order, View Customer |

#### Order Detail (`/order/read/{id}`)

**Summary cards:** Package Price, Paid Amount, PV Balance (with customer name tag), Package Balance

**Status sidebar (right):**
- PV Paid / PV Assigned / PV Balance (green badge when 0)
- Service Paid / Service Assigned / Service Balance (green/blue badge)
- Other Paid / Other Assigned / Other Balance

**Tabs:**

##### Package tab
- + Top Up button
- Order Item table: Item, Qty, Price
- Edit button (pencil icon)

##### Payment tab
- + Create Invoice button
- Payment List table: Date, Invoice No., Total (PV/SV breakdown)
- Actions per payment: VIEW, EDIT, DELETE, REFUND

##### Assign tab (Commission)
- Assign Item table: Item (with Product/Service badge), Qty, Price, Remove
- "Add Item" dropdown at bottom
- Total sum

##### Taken tab
- Items taken with: item name, price, timestamp
- Each taken record: date, branch, service type badge, staff badge, quantity
- Balance per item
- **Customer Signature** section: Date, Details, Signature table

##### Summary tab
- Text area + "Add Summary" button
- History table: Date, Details

---

### 4. Invoice (`/quoted_invoice/`)

**Filters:** Filter By Branch
**Total records:** 38,211

**Table:**
| Column | Description |
|--------|-------------|
| #Order ID | Linked order number |
| Date | Invoice date |
| Invoice No. | Invoice number (e.g. S20260713, P20260488, M20260219, FOC20260253) |
| Branch | Branch + staff |
| Customer | Customer name |
| Total Paid | Amount |
| Remarks | Payment notes (e.g. "BANK IN RHB", "ONLINE CC") |
| Action | "..." menu |

**Invoice number prefixes:**
- S = Sutera
- P = Petaling Jaya
- M = Marina
- FOC = Free of charge

---

### 5. Staff (`/staffs/`)

**Layout:** Drag-and-drop Kanban-style board

- **Left column:** Beauticians pool (all staff listed with drag handle)
- **Right columns:** Branch columns (SUTERA, NAN YANG PLACE, MARINA, PETALING JAYA)
  - Each staff shown as pink card with "x" remove button
  - Staff can be dragged between branches

---

### 6. Appointment (`/appointments/`)

**Controls:**
- Date picker with prev/next arrows
- Branch filter dropdown
- "Add Booking" button (red)
- "Change Status" button (dark)
- Calendar icon with notification badge

**Grid layout:**
- **Columns:** Staff names (per selected branch)
- **Rows:** Hourly time slots (08:00 - 16:00+)
- **Appointment cards:** Color-coded by branch, showing:
  - Branch badge
  - Customer name + member code
  - Time range (e.g. "10:30 to 13:00")
  - Remark field

**Color coding:**
- Yellow/green = SUTERA
- Green = MARINA
- Blue/light = Other branches

---

### 7. Inventory

#### 7.1 Stock Summary (`/items_inventory/branch_inventory/`)

**Filters:** Date range
**Table:** No., Product, Demo, Event Invoice, FOC, [Branch columns: Marina, Nan Yang Place, Petaling Jaya, Sutera], TOTAL

Shows quantity of each product across all branches.

#### 7.2 Stock Transaction (`/items_inventory/`)

**Actions:** + New Transaction
**Filters:** Filter By Type, Filter By Branch, All Product dropdown, Date From/To + Filter By Date Range button

**Table:**
| Column | Description |
|--------|-------------|
| No | Row number |
| Date | Transaction datetime |
| Branch | Branch + customer name |
| Amount | Quantity (+/-) |
| Type | Stock Out / To Saloon |
| Product | Product name |
| Remark | Notes (e.g. "Alex taken") |
| Action | "..." menu |

#### 7.3 Inventory Entry (`/items_inventory/inventory`)

**Filters:** Branch dropdown, Type dropdown, Input Date
**Table:** No., Product, Stock Balance (shown in dark badge), Amount (editable input), Remark (editable input)

Used for batch stock entry.

#### 7.4 Manage Product (`/items/`)

**Actions:** + New Product
**Filters:** Filter By Type

**Table:**
| Column | Description |
|--------|-------------|
| No | Row number |
| Name | Product name |
| Category | Product category |
| Minimum Unit Price | Price |
| Deleted | REMOVED badge (red) |
| Action | "..." menu |

#### 7.5 Product Category (`/items_category/`)

**Table:** No, Category, Status, Last Updated, Action

**Categories (5):**
1. Product
2. Treatment
3. Semi Permanent Embroidery
4. Chiropractic Procedure
5. Aesthetic Procedure

---

### 8. CRM

#### 8.1 Members (`/members/`)

**Actions:** + New Member
**Total records:** 13,405

**Table:**
| Column | Description |
|--------|-------------|
| # | Member ID |
| Code | IC/NRIC number |
| Name | Full name |
| Contact | Phone number |
| Birthday | Date of birth |
| Actions | "..." -> View, Edit, Delete |

#### Member Detail (`/order/create_v2/{id}`)

**Left panel - Personal info:**
- Name, Birthday (with flag icon), Contact, NRIC, Birth Place, Passport

**Wallet summary:**
- Service Wallet / Product Wallet / Total
- FOC PV / FOC SV / Total FOC
- Member Point

**MENU (quick links - icon grid):**
- Invoice
- Order
- Product
- Service
- FOC
- Summary

**Right panel:** Additional content area (context-dependent)

#### 8.2 Push Notification (`/cms_push/`)

**Actions:** + New
**Table:** No, Title, Content, Date Push, Action

---

### 9. Report

#### 9.1 Sales Report (`/reports/sales/`)

**Filters:** Branch (All Branch), Date Range

**Content:**
- **Sales Summary:** Branch-level breakdown with totals
- **Beautician Report:** Per-staff sales totals

#### 9.2 Assign Report (`/reports/assign_report/`)

**Filters:** Date range, Type (Product), Item, Branch, Customer
**Options:**
- Sort by: Branch / Customer / Item Name / Total
- Order by: Ascending / Descending
- Group by: No Group / Customer / Item
- Toggle: Hide Zero Closing Balance

#### 9.3 PVSV Report (`/reports/pvnsv_report/`)

**Actions:** Export to Excel
**Filters:** Branch, Beautician, Date From/To
**Toggles:** FOC Report, Demo Report

**Beautician summary table:** #, Beautician, Amount, PV, SV, Other, Refund, with totals
**Detail table:** No., Date, Invoice, Cust Name, Amount, PV, SV, Other, Refund

#### 9.4 Taken Report (`/reports/taken_report`)

**Actions:** Export to Excel
**Filters:** Date range, Type, Item, Branch, Customer, Beautician
**Options:**
- Sort by: Date / Branch / Beautician / Item Name / Total
- Order by: Ascending / Descending
- Group by: No Group / Date / Branch / Beautician / Item

#### 9.5 Item Sales Report (`/reports/item_sales_report/`)

**Filters:** Branch, Beautician, Item, Date From/To

**Content:**
- Summary table: #, Branch, Beautician, Total
- Detail table: No., Date, Branch, Beautician, Item, Quantity, Order ID

#### 9.6 Balance Report (`/reports/balance_report/`)

**Actions:** Export to Excel
**Filters:** Date From/To, Balance Available toggle
**Options:** Group by: No Group / Customer / Item

**Table:** Date, Customer, # Order, Item, Assigned, Taken, Balance Quantity, Balance Amount

#### 9.7 Birthday (`/reports/birthday/`)

**Table:** ID #, Member's Name (with member code tags like [Not A Member], [(M)C119], [(S)C792]), Birthday, Info (phone | email)
**Total records:** 1,008
**Pagination:** Yes

---

### 10. Master Control

#### 10.1 Users Group (`/users_group/`)

**Table:** #, Group, Edit button

**Groups (7):**
1. Customer
2. *(unnamed)*
3. Staff
4. Outlet
5. Account
6. Admin
7. Developer

#### 10.2 Staff List (`/staff/`)

**Actions:** + New Staff

**Table:**
| Column | Description |
|--------|-------------|
| # | Row number |
| Fullname | Staff full name |
| Nickname | Display name |
| Status | Active (green check) / Inactive (red x) |
| Working Hrs | Hours (e.g. 8.00, 0.00) |
| Main Outlet | Primary branch |
| Contact | Phone number |
| Manager Password | Masked (e.g. 89***) |
| Action | "..." menu |

---

## Key Business Concepts

| Concept | Description |
|---------|-------------|
| **PV (Product Value)** | Value assigned to product items in an order |
| **SV (Service Value)** | Value assigned to service items in an order |
| **FOC (Free of Charge)** | Complimentary items given to customers |
| **Package** | A bundle of products/services sold as one order |
| **Assign** | Allocating items from a package to commission tracking |
| **Taken** | Recording when a customer uses/collects assigned items |
| **Balance** | Remaining items not yet taken from an assigned package |
| **Service Wallet** | Customer's remaining service credits |
| **Product Wallet** | Customer's remaining product credits |
| **Member Point** | Loyalty points for the customer |

---

## Common UI Patterns

1. **Data tables** with pagination (server-side), dark header row
2. **Filter bars** at top of pages (Branch, Date range, Type dropdowns)
3. **Action menus** ("..." three-dot) on table rows with contextual options
4. **Status badges** (green COMPLETED, red REMOVED)
5. **Summary cards** with colored backgrounds at page tops
6. **Charts** (bar, line, pie, donut, stacked bar) using a JS charting library
7. **Drag-and-drop** for staff assignment to branches
8. **Calendar grid** for appointment scheduling
9. **Export to Excel** button on report pages
10. **Tabbed interfaces** for multi-view pages (Insight, Order Detail)
