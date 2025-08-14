---
layout: default
title: No Pricing Rules
permalink: /en/web/proposals/ePortal-roles/no-pricing-rules/
nav: false
---

{% include lang-toggle.html %}

# 🚫 No Pricing Rules

This page documents when and how to apply the `No Pricing` role to users in the new RBAC model.  
The `No Pricing` role removes all privileges related to pricing visibility:

- `U` = Unit Price  
- `L` = List Price

---

<details markdown="1">
  <summary><strong>📑 Table of Contents (click to expand)</strong></summary>

- [`When to Apply No Pricing`](#when-to-apply-no-pricing)
- [`How It Works`](#how-it-works)
- [`When Not to Apply No Pricing`](#when-not-to-apply-no-pricing)
- [`Edge Cases & Overrides`](#edge-cases--overrides)

</details>

---

## When to Apply `No Pricing` {#when-to-apply-no-pricing}

Assign the `No Pricing` role **only when the legacy group includes** the `[SH-N]` tag.

Examples of legacy groups that should receive `No Pricing`:

- `[SH-N] Order + SSP`
- `[SH-N] Gov + Warranty`
- `[SH-N] Order All + NA All + Warranty`

These groups were explicitly restricted from viewing pricing data in the legacy system.

---

## How It Works {#how-it-works}

The `No Pricing` role:

- Does **not** grant any new permissions on its own
- Acts as a filter that removes any `U` or `L` privileges granted by other roles

It supports the **Principle of Least Privilege** by ensuring users can't access pricing data unless explicitly allowed.

**Example:**

A user has:

- `Order – WH Order Submission` (includes `U`)
- `Report – Sales Report` (includes `S`)
- `No Pricing`

→ **Result:**

- `A`, `S` are kept
- `U` (Unit Price) from Order role is removed

---

## When Not to Apply `No Pricing` {#when-not-to-apply-no-pricing}

Do **not** apply the `No Pricing` role when the legacy group includes:

- `[P]` → Pricing access in general
- `[P-U]` → Unit Price
- `[P-L]` → List Price

If neither `[SH-N]` nor `[P-*]` is present, assume the default privileges from the assigned roles apply.

---

## Edge Cases & Overrides {#edge-cases--overrides}

If a user:

- Is assigned `No Pricing`, but  
- Needs pricing access for a **specific permission** (e.g., `Unit Price` for `Sales Report`)

You can either:

1. **Add a specific override role** (e.g., *Sales Report – Unit Price Only*)  
2. Use a **direct user-level override** if your system supports it (e.g., via `user_permissions`)

---

For visual examples or privilege mapping, see:  
[privilege-matrix](./privilege-matrix.md)
