---
layout: default
title: 📘 Table Definitions
permalink: /en/web/proposals/ePortal-roles/table-definitions/
nav: false
---

{% include lang-toggle.html %}

# 📘 Table Definitions

<details markdown="1">
  <summary><strong>📑 Table of Contents (click to expand)</strong></summary>

- [`users`](#users)
- [`roles`](#roles)
- [`user_roles`](#user_roles)
- [`role_corporation`](#role_corporation)
- [`role_industry_segment`](#role_industry_segment)
- [`permissions`](#permissions)
- [`privileges`](#privileges)
- [`role_permissions`](#role_permissions)

</details>

---

## `users`

Stores individual user accounts that can be assigned one or more roles. Users do not directly receive permissions or privileges — everything is inherited through assigned roles.

> ### Columns
> | Column | Type | Description |
> |--------|------|-------------|
> | `id` | INT | Primary key |
> | `email` | VARCHAR | User’s email address (unique) |
> | `name` | VARCHAR | Full name (optional) |
>
> ### Relationships
> - 🔗 `user_roles` → assigns roles to this user
>
> ### Notes
> - Users can be assigned multiple roles at once  
> - Permissions and access levels are resolved entirely through role inheritance  
> - Optional metadata like `name`, `department`, or `employee_id` can be added  

---

## `roles`

Stores reusable role templates that define a set of permission/privilege pairs. Roles are not tied to a specific user, corporation, or segment by default — they gain context through the `user_roles`, `role_corporation`, and `role_industry_segment` tables.

> ### Columns
> | Column | Type | Description |
> |--------|------|-------------|
> | `id` | INT | Unique identifier for the role |
> | `name` | VARCHAR | Display name (e.g., “Order – WH Order Submission”) |
> | `description` | TEXT | Optional explanation of the role’s purpose |
>
> ### Relationships
> - 🔗 `user_roles` → assigns this role to users  
> - 🔗 `role_permissions` → defines the permissions and privileges this role grants  
> - 🔗 `role_corporation` → scopes this role to one or more corporations  
> - 🔗 `role_industry_segment` → scopes this role to one or more industry segments  
>
> ### Notes
> - Role names are descriptive and user-readable  
> - Roles can be reused across corporations and segments unless restricted by scoping  

---

## `user_roles`

Links users to their assigned roles.

> ### Columns
> | Column | Type | Description |
> |--------|------|-------------|
> | `user_id` | INT | FK to `users.id` |
> | `role_id` | INT | FK to `roles.id` |
>
> ### Relationships
> - 🔗 `users` → defines who the role is assigned to  
> - 🔗 `roles` → defines what permissions the user receives  
>
> ### Notes
> - A user may have multiple roles (e.g., “Order Submitter” and “Report Viewer”)  
> - Roles are always assigned through this table  
> - Corporation/segment scoping is determined at the role level — not per user  

---

## `role_corporation`

Scopes a role to one or more corporations (e.g., US, CA, MX).

> ### Columns
> | Column | Type | Description |
> |--------|------|-------------|
> | `role_id` | INT | FK to `roles.id` |
> | `corporation` | VARCHAR | Country code or business unit |
>
> ### Relationships
> - 🔗 `roles` → defines which role is scoped  
>
> ### Notes
> - No entry means global access (no corp restriction)  
> - Used to enforce corporation-specific policies  
> - Codes should align with your canonical corp definitions  

---

## `role_industry_segment`

Scopes a role to one or more industry segments.

> ### Columns
> | Column | Type | Description |
> |--------|------|-------------|
> | `role_id` | INT | FK to `roles.id` |
> | `industry_segment` | VARCHAR | Segment label (e.g., “Fleet”, “Retail”) |
>
> ### Relationships
> - 🔗 `roles` → defines which role is scoped  
>
> ### Notes
> - No segment means available to all  
> - Can assign to multiple segments with multiple rows  
> - Names should be standardized across the platform  

---

## `permissions`

Represents a unique system action grouped by feature and action type.

> ### Columns
> | Column | Type | Description |
> |--------|------|-------------|
> | `id` | INT | Unique identifier for the permission |
> | `name` | VARCHAR | Canonical label |
> | `feature` | VARCHAR | Top-level category |
> | `action` | VARCHAR | Action type |
>
> ### Relationships
> - 🔗 `role_permissions` → assigns this permission to specific roles  
>
> ### Notes
> - Grouped and filterable in UI  
> - Name should remain stable across systems  
> - Reused across roles and corporations  

---

## `privileges`

Defines the level of access a user has for a given permission.

> ### Columns
> | Column | Type | Description |
> |--------|------|-------------|
> | `code` | CHAR(1) | Unique code: A, S, U, or L |
> | `label` | VARCHAR | Full name: Access, Stock, etc. |
>
> ### Relationships
> - 🔗 `role_permissions` → privileges linked to roles via permissions  
>
> ### Notes
> - Current values:  
>   - `A`: Access  
>   - `S`: Stock  
>   - `U`: Unit Price  
>   - `L`: List Price  

---

## `role_permissions`

Joins roles to permissions and defines which specific privileges apply.

> ### Columns
> | Column | Type | Description |
> |--------|------|-------------|
> | `role_id` | INT | FK to `roles.id` |
> | `permission_id` | INT | FK to `permissions.id` |
> | `privilege_code` | CHAR(1) | FK to `privileges.code` |
>
> ### Relationships
> - 🔗 `roles` → defines who the permission applies to  
> - 🔗 `permissions` → defines what action is allowed  
> - 🔗 `privileges` → defines the access level  
>
> ### Notes
> - Roles can map to the same permission multiple times with different privileges  
> - Enforces least privilege at the role level  
> - No corporate or segment scoping exists here — that comes from `role_corporation` and `role_industry_segment`  
