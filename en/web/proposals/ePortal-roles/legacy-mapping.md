---
layout: default
title: Legacy Mapping
permalink: /en/web/proposals/ePortal-roles/legacy-mapping/
nav: false
---

{% include lang-toggle.html %}

# 🗺️ Legacy Group Mapping

Mappings from legacy user group names to the new RBAC roles and privilege model. Each section lists:

- The original legacy group name and codes
- The new role(s) required to replicate access
- Any applied restrictions (like `No Pricing`)
- Notes about special handling or overrides

---

<details markdown="1">
  <summary><strong>📑 Table of Contents (click to expand)</strong></summary>

- [`(US) TCI`](#us-tci)
- [`All Permissions & No Price`](#all-permissions-no-price)
- [`Car Dealer & Secondary Supply & National Account & Warranty`](#car-dealer-secondary-supply-national-account-warranty)
- [`Order Submission & National Account & Sales Report`](#order-submission-national-account-sales-report)
- [`(US) Carroll Tire`](#us-carroll-tire)

</details>

---

## (US) TCI — `[O-WNG] [S-NG] [A] [W]` {#us-tci}

**Mapped Roles:**
- Order – WH Order Submission
- Status – Gov't & Bus
- Status – National Account
- Status – Invoice
- Warranty – Create Warranty

**Pricing Restrictions:**
- ❌ None explicitly marked; pricing assumed available where roles grant it

**Notes:**
- Pricing privileges like `U` come from specific roles (e.g., WH Order Submission)
- No `[SH-N]` or `[P]` codes present, so default behavior applies

---

## All Permissions & No Price — `[O] [S] [A] [R] [W]` {#all-permissions-no-price}

**Mapped Roles:**
- All Permissions
- No Pricing

**Pricing Restrictions:**
- ✅ Fully removed via `No Pricing` role

**Notes:**
- Full access without pricing — designed for view-only or non-commercial users
- `No Pricing` removes all `U` and `L` privileges granted by All Permissions

---

## Car Dealer & Secondary Supply & National Account & Warranty {#car-dealer-secondary-supply-national-account-warranty}

**Mapped Roles:**
- Order – Car Dealer Order
- Order – Secondary Supply Submission
- National Account – Fleet Create a New Delivery Receipt
- Warranty – Create Warranty

**Pricing Restrictions:**
- ❌ None; pricing retained where roles include it

**Notes:**
- Covers broad dealer functionality with full privilege set
- No indicators suggest pricing needs to be restricted

---

## Order Submission & National Account & Sales Report {#order-submission-national-account-sales-report}

**Mapped Roles:**
- Order – WH Order Submission
- National Account – Fleet Create a New Delivery Receipt
- Report – Sales Report

**Pricing Restrictions:**
- ❌ None; pricing retained where roles include it

**Notes:**
- Sales Report includes `A` and `S` only — does not grant `U` or `L`
- Order – WH Order Submission includes `U`, so pricing is available unless restricted

---

## (US) Carroll Tire — `[P-U] [O-SCDNG] [S-SCDNG] [W]` {#us-carroll-tire}

**Mapped Roles:**
- Order – Secondary Supply Submission
- Order – Car Dealer Order
- Order – DFC Order
- Status – Secondary Supply
- Status – Car Dealer
- Status – DFC
- Warranty – Create Warranty

**Pricing Restrictions:**
- ✅ Unit Price only (`[P-U]`)
- ❌ List Price is not granted

**Notes:**
- Legacy group was designed to give partial pricing access (unit only)
- If reuse is frequent, consider making a custom role like `Order – WH + Unit Price Only`
