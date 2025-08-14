---
layout: default
title: Role Definitions
permalink: /en/web/proposals/ePortal-roles/role-definitions/
nav: false
---

{% include lang-toggle.html %}

# 📘 Role Definitions

**ℹ️ This role catalog reflects the new RBAC model.**  
Each role in this document is informed by patterns in legacy group usage, but refactored to create clean, consistent, and reusable access bundles.  
Roles are designed for least-privilege access by default, with overrides applied only when necessary.

---

<details markdown="1">
  <summary><strong>📑 Table of Contents (click to expand)</strong></summary>

- [`Order – WH Order Submission`](#order--wh-order-submission)
- [`Order – WH Quick Order`](#order--wh-quick-order)
- [`Order – Secondary Supply Delivery Check`](#order--secondary-supply-delivery-check)
- [`Order – Secondary Supply Submission`](#order--secondary-supply-submission)
- [`Order – Car Dealer Order`](#order--car-dealer-order)
- [`Order – DFC Order`](#order--dfc-order)
- [`National Account – Fleet Create a New Delivery Receipt`](#national-account--fleet-create-a-new-delivery-receipt)
- [`National Account – Gov't & Bus`](#national-account--govt--bus)
- [`Status – Order Submission`](#status--order-submission)
- [`Status – Secondary Supply`](#status--secondary-supply)
- [`Status – Gov't & Bus`](#status--govt--bus)
- [`Status – Car Dealer`](#status--car-dealer)
- [`Status – DFC`](#status--dfc)
- [`Status – Open Items`](#status--open-items)
- [`Status – Invoice`](#status--invoice)
- [`Report – Statement`](#report--statement)
- [`Report – Sales Report`](#report--sales-report)
- [`Report – Stock Report`](#report--stock-report)
- [`Warranty – Create Warranty`](#warranty--create-warranty)
- [`Warranty – Warranty Status`](#warranty--warranty-status)
- [`All Permissions`](#all-permissions)

</details>

---

## `Order – WH Order Submission` {#order--wh-order-submission}

Grants ability to submit warehouse-based orders.  
**Permissions:** Order → WH Order Submission: A, S, U  
**Legacy Mapping:** (US) TCI - [O-WNG] [S-NG] [A] [W], Order Submission & National Account & Sales Report  
**Notes:** Often paired with Status/Report roles; add *No Pricing* if price restrictions apply.

---

## `Order – WH Quick Order` {#order--wh-quick-order}

Quick-entry ordering in the warehouse system.  
**Permissions:** Order → WH Quick Order: A, S, U

---

## `Order – Secondary Supply Delivery Check` {#order--secondary-supply-delivery-check}

Stock/delivery availability from secondary supply.  
**Permissions:** Order → Secondary Supply → Delivery Check: A

---

## `Order – Secondary Supply Submission` {#order--secondary-supply-submission}

Place orders via secondary supply networks.  
**Permissions:** Order → Secondary Supply → Order Submission: A, S, U

---

## `Order – Car Dealer Order` {#order--car-dealer-order}

Submit car dealer orders directly.  
**Permissions:** Order → Car Dealer → Order: A, S, U

---

## `Order – DFC Order` {#order--dfc-order}

Submit Direct Fulfillment Center orders.  
**Permissions:** Order → DFC Order: A

---

## `National Account – Fleet Create a New Delivery Receipt` {#national-account--fleet-create-a-new-delivery-receipt}

Initiate delivery receipts for fleet accounts.  
**Permissions:** Hankook National Fleets → Create A New Delivery Receipt: A

---

## `National Account – Gov't & Bus` {#national-account--govt--bus}

Government/business interaction via National Account channels.  
**Permissions:** Gov’t & Bus: A

---

## `Status – Order Submission` {#status--order-submission}

View status of submitted orders.  
**Permissions:** Status → Order Submission: A, S, U

---

## `Status – Secondary Supply` {#status--secondary-supply}

Track secondary supply orders.  
**Permissions:** Status → Secondary Supply: A, S, U

---

## `Status – Gov't & Bus` {#status--govt--bus}

View government/business order status.  
**Permissions:** Status → Gov’t & Bus: A

---

## `Status – Car Dealer` {#status--car-dealer}

Track car dealer orders.  
**Permissions:** Status → Car Dealer: A

---

## `Status – DFC` {#status--dfc}

Track Direct Fulfillment Center orders.  
**Permissions:** Status → DFC: A

---

## `Status – Open Items` {#status--open-items}

View unpaid/unprocessed billing items.  
**Permissions:** Status → Open Items: A

---

## `Status – Invoice` {#status--invoice}

View invoices and stock details.  
**Permissions:** Status → Invoice: A, S

---

## `Report – Statement` {#report--statement}

Access account financial statements.  
**Permissions:** Report → Statement: A

---

## `Report – Sales Report` {#report--sales-report}

View sales metrics.  
**Permissions:** Report → Sales Report: A, S

---

## `Report – Stock Report` {#report--stock-report}

View current inventory.  
**Permissions:** Report → Stock Report: A, S

---

## `Warranty – Create Warranty` {#warranty--create-warranty}

Submit new warranty claims.  
**Permissions:** Warranty Return → Create: A, S

---

## `Warranty – Warranty Status` {#warranty--warranty-status}

View warranty claim status.  
**Permissions:** Warranty Return → Status: A, S

---

## `All Permissions` {#all-permissions}

Full system access including pricing, reporting, ordering, and warranty.  
**Permissions:** All defined permissions: A, S, U, L  
**Notes:** Reserved for admins; do not assign by default.
