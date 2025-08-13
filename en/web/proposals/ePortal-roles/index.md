---
layout: default
title: "🧠 Roles & Permissions Documentation"
lang: en
permalink: /en/web/proposals/ePortal-roles/
---

{% include lang-toggle.html %}

# 🧠 Roles & Permissions Documentation

This project defines a scalable Role-Based Access Control (RBAC) structure that replaces complex legacy groupings with clean, maintainable roles and privileges. It supports edge cases, pricing restrictions, and direct overrides while preserving equivalent access levels from the legacy system.

---

## 📑 Table of Contents

- 🧠 [Overview of Roles & Permissions]({{ '/en/web/proposals/ePortal-roles/structure-overview/' | relative_url }})  
  _Visual breakdown of role categories, features, actions, business channels, and access levels._

- 📊 [RBAC Data Model]({{ '/en/web/proposals/ePortal-roles/data-model/' | relative_url }})  
  _Describes the core tables and relationships in the new roles and permissions structure._

- 🧱 [Table Definitions]({{ '/en/web/proposals/ePortal-roles/table-definitions/' | relative_url }})  
  _Detailed schema for each table including columns, relationships, and notes._

- 🧩 [Role Definitions]({{ '/en/web/proposals/ePortal-roles/role-definitions/' | relative_url }})  
  _Breakdown of all base roles and their assigned privileges._

- 🔄 [Migration Plan]({{ '/en/web/proposals/ePortal-roles/migration-plan/' | relative_url }})  
  _Step-by-step process for converting legacy groups into RBAC roles and deploying the new system._

- 🧮 [Privilege Matrix]({{ '/en/web/proposals/ePortal-roles/privilege-matrix/' | relative_url }})  
  _Maps legacy permissions to new privileges across all defined roles._

- 🧭 [Evaluation Order]({{ '/en/web/proposals/ePortal-roles/evaluation-order/' | relative_url }})  
  _Clarifies how overlapping permissions are resolved in priority order._

- 🚫 [No Pricing Rules]({{ '/en/web/proposals/ePortal-roles/no-pricing-rules/' | relative_url }})  
  _Defines restrictive rules that strip pricing privileges in specific edge cases._

- 🧾 [Legacy Mapping]({{ '/en/web/proposals/ePortal-roles/legacy-mapping/' | relative_url }})  
  _Documentation of how legacy groups are interpreted into modern roles._

- 🧷 [Direct Privileges]({{ '/en/web/proposals/ePortal-roles/direct-privileges/' | relative_url }})  
  _Guidance on granting user-specific overrides outside of role-based inheritance._
