---
layout: default
title: 데이터 모델
permalink: /ko/web/proposals/ePortal-roles/data-model/
nav: false
---

{% include lang-toggle.html %}

# RBAC 데이터 모델

이 문서는 새로운 **역할 기반 접근 제어(RBAC, Role-Based Access Control)** 시스템의 관계형 구조를 설명합니다. 여기에는 법인 스코프, 산업 세그먼트, 권한(permissions), 그리고 권한 수준(privileges) 기반 접근 제어가 포함됩니다.

<details markdown="1">
  <summary><strong>📑 목차(클릭하여 펼치기)</strong></summary>

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

## 핵심 테이블

### `users` {#users}
역할을 부여받는 시스템 사용자.

| Column | Type    | Description        |
|------:|:--------|:-------------------|
| `id`  | INT     | 기본 키            |
| `email` | VARCHAR | 사용자 이메일 주소 |

---

### `roles` {#roles}
사용자에게 부여되는 재사용 가능한 역할 템플릿(법인/세그먼트 스코프 적용).

| Column        | Type    | Description        |
|-------------:|:--------|:-------------------|
| `id`         | INT     | 기본 키            |
| `name`       | VARCHAR | 역할 표시 이름     |
| `description`| TEXT    | 선택적 설명        |

---

### `user_roles` {#user_roles}
사용자와 부여된 역할 간의 연결.

| Column    | Type | Description           |
|----------:|:-----|:----------------------|
| `user_id` | INT  | `users.id` 참조(FK)   |
| `role_id` | INT  | `roles.id` 참조(FK)   |

---

### `role_corporation` {#role_corporation}
역할을 하나 이상의 법인(예: US, CA, MX)에 스코프.

| Column        | Type    | Description                 |
|--------------:|:--------|:----------------------------|
| `role_id`     | INT     | `roles.id` 참조(FK)         |
| `corporation` | VARCHAR | 국가 코드(예: `US`)         |

---

### `role_industry_segment` {#role_industry_segment}
역할을 하나 이상의 산업 세그먼트(예: Fleet, Retail)에 스코프.

| Column             | Type    | Description            |
|-------------------:|:--------|:-----------------------|
| `role_id`          | INT     | `roles.id` 참조(FK)    |
| `industry_segment` | VARCHAR | 세그먼트 코드/라벨     |

---

### `permissions` {#permissions}
기능(feature) 하위의 고유한 동작(예: “Order Submission”).

| Column    | Type    | Description                     |
|----------:|:--------|:--------------------------------|
| `id`      | INT     | 기본 키                         |
| `name`    | VARCHAR | 권한 이름                       |
| `feature` | VARCHAR | 예: Order, Warranty, Report     |
| `action`  | VARCHAR | 예: Create, Status              |

---

### `privileges` {#privileges}
특정 권한에 부여되는 접근 수준.

| Column  | Type    | Description                           |
|--------:|:--------|:--------------------------------------|
| `code`  | CHAR(1) | `A`, `S`, `U`, `L` 중 하나            |
| `label` | VARCHAR | Access, Stock, Unit, List Price       |

---

### `role_permissions` {#role_permissions}
역할과 권한을 특정 권한 수준과 조인.

| Column           | Type    | Description                 |
|-----------------:|:--------|:----------------------------|
| `role_id`        | INT     | `roles.id` 참조(FK)         |
| `permission_id`  | INT     | `permissions.id` 참조(FK)   |
| `privilege_code` | CHAR(1) | `privileges.code` 참조(FK)  |

---

## 🧭 엔터티 관계 다이어그램

**텍스트 버전**
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

## 🔧 예시: 실제 사용 모습

사용자에게 역할 **“Order – WH Order Submission”** 이 부여되고, **US 법인**과 **Fleet 세그먼트**로 스코프되며 다음이 허용됩니다:

- **Permission:** Order Submission  
- **Feature:** Order  
- **Action:** Create  
- **Privileges:** A, S, U

---

## 🗂️ 관련 데이터 행

#### `users`
| id   | email               |
|:----:|:--------------------|
| 2001 | johndoe@example.com |

---

#### `roles`
| id | name                          |
|:--:|:------------------------------|
| 1  | Order – WH Order Submission   |

---

#### `user_roles`
| user_id | role_id |
|:-------:|:-------:|
| 2001    | 1       |

---

#### `role_corporation`
| role_id | corporation |
|:-------:|:-----------:|
| 1       | US          |

---

#### `role_industry_segment`
| role_id | industry_segment |
|:-------:|:-----------------|
| 1       | Fleet            |

---

#### `permissions`
| id  | name             | feature | action |
|:---:|:-----------------|:--------|:-------|
| 101 | Order Submission | Order   | Create |

---

#### `privileges`
| code | label       |
|:----:|:------------|
| A    | Access      |
| S    | Stock       |
| U    | Unit Price  |
| L    | List Price  |

---

#### `role_permissions`
| role_id | permission_id | privilege_code |
|:-------:|:-------------:|:--------------:|
| 1       | 101           | A              |
| 1       | 101           | S              |
| 1       | 101           | U              |

---

<details markdown="1">
  <summary>확장: 디버그 / 렌더링 확인</summary>

스타일과 마크다운 처리를 모니터링하기 위한 임시 접기 영역입니다.

```bash
echo "Hello from /ko/web/proposals/ePortal-roles/data-model.md within collapsible"
ls -la
```
</details>

### 렌더링 확인 (접기 기능 외부)

```bash
echo "Hello from /ko/web/proposals/ePortal-roles/data-model.md outside collapsible"
```
