---
layout: default
title: No Pricing 규칙
permalink: /ko/web/proposals/ePortal-roles/no-pricing-rules/
nav: false
---

{% include lang-toggle.html %}

# 🚫 No Pricing 규칙

이 페이지는 새로운 RBAC 모델에서 사용자에게 `No Pricing` 역할을 적용하는 시기와 방법을 문서화합니다.  
`No Pricing` 역할은 가격 표시와 관련된 모든 권한 수준을 제거합니다:

- `U` = 단가(Unit Price)  
- `L` = 정가(List Price)

---

<details markdown="1">
  <summary><strong>📑 목차 (클릭하여 펼치기)</strong></summary>

- [`No Pricing` 적용 시기](#when-to-apply-no-pricing)
- [`동작 방식`](#how-it-works)
- [`No Pricing`을 적용하지 말아야 할 시기](#when-not-to-apply-no-pricing)
- [`예외 및 재정의`](#edge-cases--overrides)

</details>

---

## `No Pricing` 적용 시기 {#when-to-apply-no-pricing}

레거시 그룹에 `[SH-N]` 태그가 **포함된 경우에만** `No Pricing` 역할을 부여합니다.

`No Pricing`이 적용되어야 하는 레거시 그룹 예시:

- `[SH-N] Order + SSP`
- `[SH-N] Gov + Warranty`
- `[SH-N] Order All + NA All + Warranty`

이러한 그룹은 레거시 시스템에서 가격 데이터를 볼 수 없도록 명시적으로 제한되었습니다.

---

## 동작 방식 {#how-it-works}

`No Pricing` 역할은:

- 자체적으로 새로운 권한을 **부여하지 않음**
- 다른 역할이 부여한 `U` 또는 `L` 권한을 제거하는 필터 역할 수행

이는 사용자가 명시적으로 허용되지 않는 한 가격 데이터를 접근할 수 없도록 하는 **최소 권한 원칙**을 지원합니다.

**예시:**

사용자 역할:

- `Order – WH Order Submission` (`U` 포함)
- `Report – Sales Report` (`S` 포함)
- `No Pricing`

→ **결과:**

- `A`, `S`는 유지  
- Order 역할에서 부여된 `U`(단가)는 제거

---

## `No Pricing`을 적용하지 말아야 할 시기 {#when-not-to-apply-no-pricing}

레거시 그룹에 다음이 포함된 경우 `No Pricing` 역할을 적용하지 않습니다:

- `[P]` → 일반 가격 접근
- `[P-U]` → 단가(Unit Price)
- `[P-L]` → 정가(List Price)

`[SH-N]` 또는 `[P-*]`가 없는 경우, 할당된 역할의 기본 권한 수준이 적용된다고 가정합니다.

---

## 예외 및 재정의 {#edge-cases--overrides}

다음과 같은 경우:

- `No Pricing`이 할당되었지만  
- **특정 권한**에 대한 가격 접근이 필요한 경우 (예: `Sales Report`의 `단가`)

다음 중 하나를 수행할 수 있습니다:

1. **특정 재정의 역할 추가** (예: *Sales Report – Unit Price Only*)  
2. 시스템에서 지원하는 경우 **사용자 수준 직접 재정의** 사용 (예: `user_permissions`를 통한 적용)

---

시각적 예시 또는 권한 수준 매핑은 다음을 참조하세요:  
[privilege-matrix](./privilege-matrix.md)
