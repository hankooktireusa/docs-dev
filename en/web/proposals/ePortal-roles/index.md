---
layout: default
title: ePortal Roles
permalink: /en/web/proposals/ePortal-roles/
nav: false
---

{% include lang-toggle.html %}

# Roles & Permissions Documentation

This project defines a scalable **Role-Based Access Control (RBAC)** structure that replaces complex legacy groupings with clean, maintainable roles and privileges. It supports edge cases, pricing restrictions, and direct overrides while preserving equivalent access levels from the legacy system.

---

## Table of Contents
- [Overview of Roles & Permissions](./structure-overview/)  
  *Visual breakdown of role categories, features, actions, business channels, and access levels.*
- [RBAC Data Model](./data-model/)  
  *Core tables and relationships in the new roles and permissions structure.*
- [Table Definitions](./table-definitions/)  
  *Detailed schema for each table including columns, relationships, and notes.*
- [Role Definitions](./role-definitions/)  
  *All base roles and their assigned privileges.*
- [Migration Plan](./migration-plan/)  
  *Step-by-step process for converting legacy groups into RBAC roles and deploying the new system.*
- [Privilege Matrix](./privilege-matrix/)  
  *Maps legacy permissions to new privileges across all defined roles.*
- [Evaluation Order](./evaluation-order/)  
  *How overlapping permissions are resolved in priority order.*
- [No Pricing Rules](./no-pricing-rules/)  
  *Restrictive rules that remove pricing privileges in specific edge cases.*
- [Legacy Mapping](./legacy-mapping/)  
  *How legacy groups map into modern roles.*
- [Direct Privileges](./direct-privileges/)  
  *Guidance on user-specific overrides outside of role inheritance.*

---

<details markdown="1">
  <summary>Expand: Debug / Render checks</summary>

Temporary collapsible to monitor styling and markdown processing.

```bash
echo "Hello from /en/web/proposals/ePortal-roles/index.md within collapsible"
ls -la
```
</details>

### Render Sanity Check (outside collapsible)

```bash
echo "Hello from /en/web/proposals/ePortal-roles/index.md outside collapsible"
```
