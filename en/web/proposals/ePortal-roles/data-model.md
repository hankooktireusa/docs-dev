---
layout: default
title: Data Model
permalink: /en/web/proposals/ePortal-roles/data-model/
nav: false
---

{% include lang-toggle.html %}

# RBAC Data Model

This document describes the relational structure of the new **Role-Based Access Control (RBAC)** system, including support for corporations, industry segments, permissions, and privilege-based access levels.

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

## Core Tables

### `users` {#users}
Represents system users who are assigned roles.

| Column | Type   | Description        |
|-------:|:-------|:-------------------|
| `id`   | INT    | Primary key        |
| `email`| VARCHAR| User email address |

---

### `roles` {#roles}
Reusable role templates assigned to users and scoped to corporations and segments.

| Column       | Type   | Description          |
|-------------:|:-------|:---------------------|
| `id`         | INT    | Primary key          |
| `name`       | VARCHAR| Role display name    |
| `description`| TEXT   | Optional description |

---

### `user_roles` {#user_roles}
Links users to their assigned roles.

| Column     | Type | Description            |
|-----------:|:-----|:-----------------------|
| `user_id`  | INT  | FK to `users.id`       |
| `role_id`  | INT  | FK to `roles.id`       |

---

### `role_corporation` {#role_corporation}
Scopes roles to one or more corporations (e.g., US, CA, MX).

| Column        | Type    | Description                    |
|--------------:|:--------|:-------------------------------|
| `role_id`     | INT     | FK to `roles.id`               |
| `corporation` | VARCHAR | Country code (e.g., `US`)      |

---

### `role_industry_segment` {#role_industry_segment}
Scopes roles to one or more industry segments (e.g., Fleet, Retail).

| Column             | Type    | Description              |
|-------------------:|:--------|:-------------------------|
| `role_id`          | INT     | FK to `roles.id`         |
| `industry_segment` | VARCHAR | Segment code or label    |

---

### `permissions` {#permissions}
Represents a unique action under a feature (e.g., “Order Submission”).

| Column       | Type    | Description                        |
|-------------:|:--------|:-----------------------------------|
| `id`         | INT     | Primary key                        |
| `name`       | VARCHAR | Permission name                    |
| `feature`    | VARCHAR | e.g., Order, Warranty, Report      |
| `action`     | VARCHAR | e.g., Create, Status               |

---

### `privileges` {#privileges}
Defines the level of access granted to a permission.

| Column     | Type    | Description                               |
|-----------:|:--------|:------------------------------------------|
| `code`     | CHAR(1) | One of: `A`, `S`, `U`, `L`                |
| `label`    | VARCHAR | Access, Stock, Unit, List Price           |

---

### `role_permissions` {#role_permissions}
Joins roles to permissions with specific privileges.

| Column          | Type    | Description                    |
|----------------:|:--------|:-------------------------------|
| `role_id`       | INT     | FK to `roles.id`               |
| `permission_id` | INT     | FK to `permissions.id`         |
| `privilege_code`| CHAR(1) | FK to `privileges.code`        |

---

## 🧭 Entity Relationship Diagram

**Text Version**
```
           ┌───────────┐
           │   users   │
           └─────┬─────┘
                 │
                 ▼
          ┌──────────────┐
          │  user_roles  │
          └────┬────┬────┘
               │    │
               ▼    ▼
           ┌───────────┐
           │   roles   │
           └───┬──┬──┬─┘
               │  │  └───────────────────────────────────────────┐
               │  └─────────────────────┐                        │
               ▼                        ▼                        ▼
     ┌──────────────────┐ ┌──────────────────────────────┐ ┌────────────────────┐
     │ role_corporation │ │ role_industry_segment        │ │  role_permissions  │
     └──────────────────┘ └──────────────────────────────┘ └──────────┬─────────┘
                                                                      │
                                                                      ▼
                                                               ┌─────────────┐
                                                               │ permissions │
                                                               └──────┬──────┘
                                                                      │
                                                                      ▼
                                                                ┌────────────┐
                                                                │ privileges │
                                                                └────────────┘
```

---

## 🔧 Example: What This Looks Like in Practice

A user is assigned the role **“Order – WH Order Submission”**, scoped to the **US Corporation** and **Fleet Segment**, and is granted:

- **Permission:** Order Submission  
- **Feature:** Order  
- **Action:** Create  
- **Privileges:** A, S, U

---

## 🗂️ Data Rows Involved

#### `users`
<!-- table -->

| id   | email               |
|-----:|:--------------------|
| 2001 | johndoe@example.com |

---

#### `roles`
<!-- table -->

| id | name                        |
|---:|:----------------------------|
| 1  | Order – WH Order Submission |

---

#### `user_roles`
<!-- table -->

| user_id | role_id |
|:-------:|:-------:|
| 2001    | 1       |

---

#### `role_corporation`
<!-- table -->

| role_id | corporation |
|:-------:|:-----------:|
| 1       | US          |

---

#### `role_industry_segment`
<!-- table -->

| role_id | industry_segment |
|:-------:|:-----------------|
| 1       | Fleet            |

---

#### `permissions`
<!-- table -->

| id  | name             | feature | action |
|:---:|:-----------------|:--------|:-------|
| 101 | Order Submission | Order   | Create |

---

#### `privileges`
<!-- table -->

| code | label      |
|:----:|:-----------|
| A    | Access     |
| S    | Stock      |
| U    | Unit Price |
| L    | List Price |

---

#### `role_permissions`
<!-- table -->

| role_id | permission_id | privilege_code |
|:-------:|:-------------:|:--------------:|
| 1       | 101           | A              |
| 1       | 101           | S              |
| 1       | 101           | U              |

---

<details markdown="1">
  <summary>Expand: Debug / Render checks</summary>

Temporary collapsible to monitor styling and markdown processing.

```bash
echo "Hello from /en/web/proposals/ePortal-roles/data-model.md within collapsible"
ls -la
```
</details>

### Render Sanity Check (outside collapsible)

```bash
echo "Hello from /en/web/proposals/ePortal-roles/data-model.md outside collapsible"
```
