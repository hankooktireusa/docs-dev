---
layout: default
title: 권한 매트릭스
permalink: /ko/web/proposals/ePortal-roles/privilege-matrix/
nav: false
---

{% include lang-toggle.html %}

# 📊 권한 매트릭스

역할 전반에서 사용되는 모든 권한과 각 권한이 노출하는 권한 수준(Privileges)을 전체 매트릭스로 제공합니다.

**ℹ️ 참고:** 이 매트릭스는 새로운 RBAC 역할 모델에서 정의된 권한 수준을 반영합니다.  
아래에 나열된 각 권한은 [role-definitions](./role-definitions.md)에 설명된 역할에서의 사용 방식에 따라 `A`, `S`, `U`, `L` 권한에 매핑됩니다.  
이 문서는 향후 감사, 재정의 로직, 역할 설계 결정을 지원하기 위한 것이며, 과거 그룹 사용 내역을 반영하지 않습니다.

---

<details markdown="1">
  <summary><strong>📑 목차 (클릭하여 펼치기)</strong></summary>

- [`주문`](#order)
- [`내셔널 어카운트`](#national-account)
- [`상태`](#status)
- [`보고서`](#report)
- [`보증`](#warranty)
- [`모든 권한`](#all-permissions)

</details>

---

**A** = 접근(Access)  
**S** = 재고(Stock)  
**U** = 단가(Unit Price)  
**L** = 정가(List Price)  

---

## `주문` {#order}

| 권한                                       | A   | S   | U   | L   |
|--------------------------------------------|:---:|:---:|:---:|:---:|
| WH Order → Order Submission                | ✅  | ✅  | ✅  |     |
| WH Order → Quick Order                     | ✅  | ✅  | ✅  |     |
| Secondary Supply → Delivery Check          | ✅  |     |     |     |
| Secondary Supply → Order Submission        | ✅  | ✅  | ✅  |     |
| Car Dealer → Order                         | ✅  | ✅  | ✅  |     |
| DFC Order                                  | ✅  |     |     |     |

---

## `내셔널 어카운트` {#national-account}

| 권한                                                   | A   | S   | U   | L   |
|--------------------------------------------------------|:---:|:---:|:---:|:---:|
| Hankook National Fleets → Create A New Delivery Receipt | ✅  |     |     |     |
| Gov't & Bus                                             | ✅  |     |     |     |

---

## `상태` {#status}

| 권한                  | A   | S   | U   | L   |
|-----------------------|:---:|:---:|:---:|:---:|
| Order Submission      | ✅  | ✅  | ✅  |     |
| Secondary Supply      | ✅  | ✅  | ✅  |     |
| Gov't & Bus           | ✅  |     |     |     |
| Car Dealer            | ✅  |     |     |     |
| DFC                   | ✅  |     |     |     |
| Open Items            | ✅  |     |     |     |
| Invoice               | ✅  | ✅  |     |     |

---

## `보고서` {#report}

| 권한           | A   | S   | U   | L   |
|----------------|:---:|:---:|:---:|:---:|
| Statement      | ✅  |     |     |     |
| Sales Report   | ✅  | ✅  |     |     |
| Stock Report   | ✅  | ✅  |     |     |

---

## `보증` {#warranty}

| 권한             | A   | S   | U   | L   |
|------------------|:---:|:---:|:---:|:---:|
| Create Warranty  | ✅  | ✅  |     |     |
| Warranty Status  | ✅  | ✅  |     |     |

---

## `모든 권한` {#all-permissions}

| 권한               | A   | S   | U   | L   |
|--------------------|:---:|:---:|:---:|:---:|
| All of the above   | ✅  | ✅  | ✅  | ✅  |
