---
layout: default
title: RBAC Structure Overview
permalink: /en/web/proposals/ePortal-roles/structure-overview/
nav: false
---

{% include lang-toggle.html %}

# 🧠 RBAC Structure Overview

## Overview of the Object Structure

```yaml
Corporation: [COUNTRY]
└── Industry Segment: [Segment]
    └── Feature: [Feature]
        └── Action Type: [Create | Status]
            ├── Business Channel: [Channel 1]
            │   └── Access Level: [A/S/U/L]
            └── Business Channel: [Channel 2]
                └── Access Level: [A/S/U/L]
```

## Categories

<details markdown="1">
<summary>🏢 Corporations</summary>

- US
- CA
- MX
- PA
- CO
- CL
</details>

<details markdown="1">
<summary>🏭 Industry Segments</summary>

<details markdown="1">
<summary>Wholesale</summary>
**Features:** Order, Claims, Returns, Warranty Return, Finance, Report
</details>

<details markdown="1">
<summary>Retail</summary>
**Features:** Order, Claims, Returns, Warranty Return, Finance, Report
</details>

<details markdown="1">
<summary>Fleet</summary>
**Features:** Order, Claims, Returns, Warranty Return, Finance, Report
</details>

<details markdown="1">
<summary>Insurance</summary>
**Features:** Order, Claims, Returns, Warranty Return, Finance, Report
</details>

<details markdown="1">
<summary>Commercial</summary>
**Features:** Order, Claims, Returns, Warranty Return, Finance, Report
</details>

<details markdown="1">
<summary>Wholesale + Retail</summary>
**Features:** Order, Claims, Returns, Warranty Return, Finance, Report
</details>
</details>

<details markdown="1">
<summary>📁 Features</summary>

<details markdown="1">
<summary>Order</summary>
**Action:** Create, Status
</details>

<details markdown="1">
<summary>Claims</summary>
**Action:** Create, Status
</details>

<details markdown="1">
<summary>Returns</summary>
**Action:** Create, Status
</details>

<details markdown="1">
<summary>Warranty Return</summary>
**Action:** Create, Status
</details>

<details markdown="1">
<summary>Finance</summary>
**Action:** Create, Status
</details>

<details markdown="1">
<summary>Report</summary>
**Action:** Create, Status
</details>
</details>

<details markdown="1">
<summary>🎯 Actions</summary>

- Create
- Status
</details>

<details markdown="1">
<summary>🧭 Business Channels</summary>

- WH (Warehouse)
- SSP (Secondary Supply)
- CDTP (Car Dealer)
- DFC
- NAP (National Account Program)
- Gov't & Bus
</details>

<details markdown="1">
<summary>🔐 Access Levels</summary>

- Access (A)
- Stock (S)
- Unit Price (U)
- List Price (L)
</details>

## 🧪 Examples

```yaml
Corporation: US
└── Industry Segment: Fleet
    └── Feature: Order
        └── Action Type: Create
            ├── Business Channel: WH
            │   └── Access Level: A, S, U
            └── Business Channel: DFC
                └── Access Level: A
```

```yaml
Corporation: US
    ├── Industry Segment: Fleet
    │   ├── Feature: Order
    │   │   ├── Action Type: Create
    │   │   │   ├── Business Channel: WH
    │   │   │   │   └── Access Level: A, S, U
    │   │   │   └── Business Channel: DFC
    │   │   │       └── Access Level: A
    │   │   └── Action Type: Status
    │   │       └── Business Channel: WH
    │   │           └── Access Level: A, S
    │   ├── Feature: Warranty Return
    │   │   ├── Action Type: Create
    │   │   │   └── Business Channel: WH
    │   │   │       └── Access Level: A, S
    │   │   └── Action Type: Status
    │   │       └── Business Channel: WH
    │   │           └── Access Level: A, S
    │   └── Feature: Report
    │       └── Action Type: Status
    │           ├── Business Channel: Sales Report
    │           │   └── Access Level: A, S
    │           └── Business Channel: Stock Report
    │               └── Access Level: A, S
    └── Industry Segment: Retail
        ├── Feature: Order
        │   ├── Action Type: Create
        │   │   ├── Business Channel: SSP
        │   │   │   └── Access Level: A
        │   │   └── Business Channel: CDTP
        │   │       └── Access Level: A, S, U
        │   └── Action Type: Status
        │       └── Business Channel: CDTP
        │           └── Access Level: A
        └── Feature: Report
            └── Action Type: Status
                └── Business Channel: Statement
                    └── Access Level: A
```
