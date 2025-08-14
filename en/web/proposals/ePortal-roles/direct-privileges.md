---
layout: default
title: Direct Privileges
permalink: /en/web/proposals/ePortal-roles/direct-privileges/
nav: false
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">
{% include lang-toggle.html %}

# 🧩 Direct Privilege Grants

This document explains how to apply individual permission and privilege overrides directly to a user, outside of their assigned roles.  
Direct grants should be used sparingly — only when roles and filters (like `No Pricing`) are insufficient.

---

<details>
  <summary><strong>📑 Table of Contents (click to expand)</strong></summary>

- [When to Use Direct Grants](#when-to-use-direct-grants)
- [How Direct Grants Work](#how-direct-grants-work)
- [Examples](#examples)
- [Best Practices](#best-practices)

</details>

---

## When to Use Direct Grants

Use a direct grant when:

- A user needs **just one extra permission or privilege**
- You need to **override a `No Pricing` role** for a specific case
- A legacy group had an uncommon combination not worth turning into a reusable role

---

## How Direct Grants Work

Direct grants are stored per user, alongside (but separate from) their roles. They allow you to:

- Add or override specific privileges (`A`, `S`, `U`, `L`) for a given permission
- Either supplement or override inherited role-based permissions

They are evaluated **after** roles and filters like `No Pricing`.

---

## Examples

### ✅ Example 1: Add Unit Price for Sales Report only

**User roles:**

- `Report – Sales Report` (grants `A`, `S`)
- `No Pricing` (removes `U`, `L`)

→ **Add direct grant:**
```text
User: jdoe
Permission: Report → Sales Report
Privileges: U
```

**Now the user has:**

- `A`, `S` from role  
- `U` from direct grant  
- `L` still removed via `No Pricing`  

---

### ✅ Example 2: Custom invoice access

User doesn't need `Invoice` role, just wants to view stock-level invoice data.

→ **Add direct grant:**
```text
User: jsmith
Permission: Status → Invoice
Privileges: A, S
```

---

## Best Practices

- ✅ Use direct grants only for **rare exceptions**
- ❌ Do not replace roles with direct grants
- 🔐 Always log and review direct grants regularly
- 🔄 Prefer to update roles or create small custom roles if multiple users need the same override

---

For standard permissions and privilege exposure, see:

- [role-definitions](./role-definitions.md)
- [privilege-matrix](./privilege-matrix.md)
