---
layout: default
title: Privilege Matrix
permalink: /en/web/proposals/ePortal-roles/privilege-matrix/
nav: false
---

{% include lang-toggle.html %}

# 📊 Privilege Matrix

A full matrix of all permissions used across roles, showing which privilege levels each permission exposes.

**ℹ️ Note:** This matrix reflects the privilege levels defined by the new RBAC role model.  
Each permission listed below maps to the `A`, `S`, `U`, and `L` privileges based on how it is used in the roles described in [role-definitions](./role-definitions.md).  
This document is forward-looking and intended to support auditing, override logic, and role design decisions. It does not reflect historical group usage.

---

<details markdown="1">
  <summary><strong>📑 Table of Contents (click to expand)</strong></summary>

- [`Order`](#order)
- [`National Account`](#national-account)
- [`Status`](#status)
- [`Report`](#report)
- [`Warranty`](#warranty)
- [`All Permissions`](#all-permissions)

</details>

---

**A** = Access  
**S** = Stock  
**U** = Unit Price  
**L** = List Price  

---

## `Order` {#order}

| Permission                                | A   | S   | U   | L   |
|-------------------------------------------|:---:|:---:|:---:|:---:|
| WH Order → Order Submission               | ✅  | ✅  | ✅  |     |
| WH Order → Quick Order                    | ✅  | ✅  | ✅  |     |
| Secondary Supply → Delivery Check         | ✅  |     |     |     |
| Secondary Supply → Order Submission       | ✅  | ✅  | ✅  |     |
| Car Dealer → Order                        | ✅  | ✅  | ✅  |     |
| DFC Order                                 | ✅  |     |     |     |

---

## `National Account` {#national-account}

| Permission                                           | A   | S   | U   | L   |
|------------------------------------------------------|:---:|:---:|:---:|:---:|
| Hankook National Fleets → Create A New Delivery Receipt | ✅  |     |     |     |
| Gov't & Bus                                           | ✅  |     |     |     |

---

## `Status` {#status}

| Permission              | A   | S   | U   | L   |
|-------------------------|:---:|:---:|:---:|:---:|
| Order Submission        | ✅  | ✅  | ✅  |     |
| Secondary Supply        | ✅  | ✅  | ✅  |     |
| Gov't & Bus             | ✅  |     |     |     |
| Car Dealer              | ✅  |     |     |     |
| DFC                     | ✅  |     |     |     |
| Open Items              | ✅  |     |     |     |
| Invoice                 | ✅  | ✅  |     |     |

---

## `Report` {#report}

| Permission     | A   | S   | U   | L   |
|----------------|:---:|:---:|:---:|:---:|
| Statement      | ✅  |     |     |     |
| Sales Report   | ✅  | ✅  |     |     |
| Stock Report   | ✅  | ✅  |     |     |

---

## `Warranty` {#warranty}

| Permission       | A   | S   | U   | L   |
|------------------|:---:|:---:|:---:|:---:|
| Create Warranty  | ✅  | ✅  |     |     |
| Warranty Status  | ✅  | ✅  |     |     |

---

## `All Permissions` {#all-permissions}

| Permission         | A   | S   | U   | L   |
|--------------------|:---:|:---:|:---:|:---:|
| All of the above   | ✅  | ✅  | ✅  | ✅  |
