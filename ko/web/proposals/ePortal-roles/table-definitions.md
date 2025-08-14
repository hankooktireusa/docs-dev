---
layout: default
title: 📘 테이블 정의
permalink: /ko/web/proposals/ePortal-roles/table-definitions/
nav: false
---

{% include lang-toggle.html %}

# 📘 테이블 정의

<details markdown="1">
  <summary><strong>📑 목차 (클릭하여 펼치기)</strong></summary>

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

개별 사용자 계정을 저장합니다. 각 사용자는 하나 이상의 역할을 부여받을 수 있습니다. 권한과 권한 수준은 직접 부여되지 않고, 할당된 역할을 통해 상속됩니다.

> ### 컬럼
> | 컬럼 | 타입 | 설명 |
> |------|------|------|
> | `id` | INT | 기본 키 |
> | `email` | VARCHAR | 사용자의 이메일 주소 (고유) |
> | `name` | VARCHAR | 전체 이름 (선택 사항) |
>
> ### 관계
> - 🔗 `user_roles` → 이 사용자에게 역할을 부여
>
> ### 비고
> - 사용자는 동시에 여러 역할을 가질 수 있음  
> - 권한과 접근 수준은 전적으로 역할 상속을 통해 결정됨  
> - `name`, `department`, `employee_id`와 같은 선택적 메타데이터를 추가할 수 있음  

---

## `roles`

권한/권한 수준 쌍을 정의하는 재사용 가능한 역할 템플릿을 저장합니다. 역할은 기본적으로 특정 사용자, 법인, 산업 세그먼트에 연결되지 않으며, `user_roles`, `role_corporation`, `role_industry_segment` 테이블을 통해 컨텍스트를 가집니다.

> ### 컬럼
> | 컬럼 | 타입 | 설명 |
> |------|------|------|
> | `id` | INT | 역할의 고유 식별자 |
> | `name` | VARCHAR | 표시 이름 (예: “Order – WH 주문 제출”) |
> | `description` | TEXT | 역할의 목적에 대한 선택적 설명 |
>
> ### 관계
> - 🔗 `user_roles` → 사용자를 역할에 할당  
> - 🔗 `role_permissions` → 이 역할이 부여하는 권한과 권한 수준을 정의  
> - 🔗 `role_corporation` → 이 역할을 하나 이상의 법인에 한정  
> - 🔗 `role_industry_segment` → 이 역할을 하나 이상의 산업 세그먼트에 한정  
>
> ### 비고
> - 역할 이름은 설명적이고 사용자 친화적으로 작성  
> - 한정 조건이 없으면 역할은 여러 법인 및 세그먼트에서 재사용 가능  

---

## `user_roles`

사용자와 부여된 역할을 연결합니다.

> ### 컬럼
> | 컬럼 | 타입 | 설명 |
> |------|------|------|
> | `user_id` | INT | `users.id`의 FK |
> | `role_id` | INT | `roles.id`의 FK |
>
> ### 관계
> - 🔗 `users` → 역할이 부여된 사용자  
> - 🔗 `roles` → 사용자가 받는 권한  
>
> ### 비고
> - 사용자는 여러 역할을 가질 수 있음 (예: “주문 제출자”, “보고서 뷰어”)  
> - 역할은 항상 이 테이블을 통해 부여됨  
> - 법인/세그먼트 한정은 사용자 단위가 아닌 역할 단위에서 결정됨  

---

## `role_corporation`

역할을 하나 이상의 법인(예: US, CA, MX)에 한정합니다.

> ### 컬럼
> | 컬럼 | 타입 | 설명 |
> |------|------|------|
> | `role_id` | INT | `roles.id`의 FK |
> | `corporation` | VARCHAR | 국가 코드 또는 사업 부문 |
>
> ### 관계
> - 🔗 `roles` → 한정할 역할  
>
> ### 비고
> - 항목이 없으면 전역 접근 가능 (법인 제한 없음)  
> - 법인별 정책을 강제하는 데 사용  
> - 코드는 표준 법인 정의와 일치해야 함  

---

## `role_industry_segment`

역할을 하나 이상의 산업 세그먼트에 한정합니다.

> ### 컬럼
> | 컬럼 | 타입 | 설명 |
> |------|------|------|
> | `role_id` | INT | `roles.id`의 FK |
> | `industry_segment` | VARCHAR | 세그먼트 라벨 (예: “Fleet”, “Retail”) |
>
> ### 관계
> - 🔗 `roles` → 한정할 역할  
>
> ### 비고
> - 세그먼트가 없으면 모든 세그먼트에 사용 가능  
> - 여러 행을 통해 여러 세그먼트에 할당 가능  
> - 세그먼트 이름은 플랫폼 전반에서 표준화 필요  

---

## `permissions`

기능과 작업 유형별로 그룹화된 고유한 시스템 동작을 나타냅니다.

> ### 컬럼
> | 컬럼 | 타입 | 설명 |
> |------|------|------|
> | `id` | INT | 권한의 고유 식별자 |
> | `name` | VARCHAR | 표준 라벨 |
> | `feature` | VARCHAR | 최상위 기능 범주 |
> | `action` | VARCHAR | 작업 유형 |
>
> ### 관계
> - 🔗 `role_permissions` → 이 권한을 특정 역할에 부여  
>
> ### 비고
> - UI에서 그룹화 및 필터링 가능  
> - 권한 이름은 시스템 간에 안정적으로 유지  
> - 여러 역할과 법인에서 재사용 가능  

---

## `privileges`

특정 권한에 대해 사용자가 가지는 접근 수준을 정의합니다.

> ### 컬럼
> | 컬럼 | 타입 | 설명 |
> |------|------|------|
> | `code` | CHAR(1) | 고유 코드: A, S, U, 또는 L |
> | `label` | VARCHAR | 전체 명칭: Access, Stock 등 |
>
> ### 관계
> - 🔗 `role_permissions` → 권한을 통해 역할과 연결된 권한 수준  
>
> ### 비고
> - 현재 값:  
>   - `A`: Access  
>   - `S`: Stock  
>   - `U`: Unit Price  
>   - `L`: List Price  

---

## `role_permissions`

역할과 권한을 연결하고, 적용되는 특정 권한 수준을 정의합니다.

> ### 컬럼
> | 컬럼 | 타입 | 설명 |
> |------|------|------|
> | `role_id` | INT | `roles.id`의 FK |
> | `permission_id` | INT | `permissions.id`의 FK |
> | `privilege_code` | CHAR(1) | `privileges.code`의 FK |
>
> ### 관계
> - 🔗 `roles` → 권한이 적용되는 역할  
> - 🔗 `permissions` → 허용되는 작업  
> - 🔗 `privileges` → 접근 수준  
>
> ### 비고
> - 동일한 권한에 대해 다른 권한 수준을 적용하여 여러 번 매핑 가능  
> - 역할 단위에서 최소 권한 원칙을 적용  
> - 법인 또는 세그먼트 한정은 여기서 정의하지 않음 — 이는 `role_corporation` 및 `role_industry_segment`에서 결정됨  
