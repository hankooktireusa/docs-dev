---
layout: default
title: Migration Plan
permalink: /en/web/proposals/ePortal-roles/migration-plan/
nav: false
---

{% include lang-toggle.html %}

# 🔄 Role Onboarding Plan: New RBAC Implementation

This plan outlines how to roll out the new Role-Based Access Control (RBAC) system for a new platform.  
The new structure preserves the same access patterns users had in legacy systems, but delivers them through a cleaner, more standardized, and more maintainable model.

---

<details markdown="1">
  <summary><strong>📑 Table of Contents (click to expand)</strong></summary>

- [`📌 Phase 1: Access Pattern Analysis`](#phase-1-access-pattern-analysis)
- [`📌 Phase 2: Role Design Finalization`](#phase-2-role-design-finalization)
- [`📌 Phase 3: Initial User Role Assignment`](#phase-3-initial-user-role-assignment)
- [`📌 Phase 4: Testing & Verification`](#phase-4-testing--verification)
- [`📌 Phase 5: Production Deployment`](#phase-5-production-deployment)
- [`🧩 Notes`](#notes)

</details>

---

## 📌 Phase 1: Access Pattern Analysis {#phase-1-access-pattern-analysis}

*Goal:* Identify required access patterns and permission sets for all user types on the new site.

**✅ Steps:**
1. **Define user personas and business functions**
2. **List all required permissions and associated privilege levels**
3. **Map common combinations to potential roles**
4. **Document special or restricted scenarios** (e.g., no pricing)

---

## 📌 Phase 2: Role Design Finalization {#phase-2-role-design-finalization}

*Goal:* Build a clean set of roles in [role-definitions](./role-definitions.md) that reflect all standard access needs.

**✅ Steps:**
1. **Define base roles** for each key function (e.g., Order Submitter, Fleet Viewer)
2. **Incorporate scoping logic** (e.g., region, segment) where needed
3. Add modifier roles like `No Pricing` or `Report Only`
4. Ensure role coverage meets all documented access needs

---

## 📌 Phase 3: Initial User Role Assignment {#phase-3-initial-user-role-assignment}

*Goal:* Assign users to roles based on their expected use cases for the new platform.

**✅ Steps:**
1. Assign one or more roles per user based on persona
2. Use scoped roles where applicable (e.g., Fleet CA only)
3. Apply restrictive roles as needed (e.g., `No Pricing`)
4. Document any direct overrides used for edge cases

---

## 📌 Phase 4: Testing & Verification {#phase-4-testing--verification}

*Goal:* Ensure all roles provide intended access and restrictions work correctly.

**✅ Steps:**
1. Test all base roles against sample users
2. Verify scoping behavior in different contexts
3. Check behavior of restrictive roles (`No Pricing`, etc.)
4. Log and address any unexpected access gaps or overreach

---

## 📌 Phase 5: Production Deployment {#phase-5-production-deployment}

*Goal:* Launch the RBAC system on the new platform with clean tracking and observability.

**✅ Steps:**
1. Enable role-based access enforcement in the new site
2. Monitor activity and behavior across user types
3. Track and resolve feedback or edge case access issues
4. Plan periodic access reviews to validate assignments

---

## 🧩 Notes {#notes}

- This RBAC model supports the same level of access users had in legacy systems, but with a **more structured, maintainable, and transparent approach**.
- The `All Permissions` role can be used for administrative or all-access needs.
- Restrictive roles (e.g., `No Pricing`) provide global access controls.
- Direct privilege overrides are supported but should be used sparingly and logged.
