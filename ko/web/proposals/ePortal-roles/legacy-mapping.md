---
layout: default
title: 레거시 매핑
permalink: /ko/web/proposals/ePortal-roles/legacy-mapping/
nav: false
---

{% include lang-toggle.html %}

# 🗺️ 레거시 그룹 매핑

레거시 사용자 그룹 이름을 새로운 RBAC 역할 및 권한 수준 모델로 매핑한 내용입니다. 각 섹션에는 다음이 포함됩니다:

- 원래 레거시 그룹 이름 및 코드
- 동일한 접근을 재현하기 위해 필요한 새 역할
- 적용된 제한 사항(`No Pricing` 등)
- 특수 처리 또는 재정의에 대한 참고 사항

---

<details markdown="1">
  <summary><strong>📑 목차 (클릭하여 펼치기)</strong></summary>

- [`(US) TCI`](#us-tci)
- [`모든 권한 & 가격 없음`](#all-permissions-no-price)
- [`자동차 딜러 & 2차 공급 & 내셔널 어카운트 & 보증`](#car-dealer-secondary-supply-national-account-warranty)
- [`주문 제출 & 내셔널 어카운트 & 판매 보고서`](#order-submission-national-account-sales-report)
- [`(US) 캐롤 타이어`](#us-carroll-tire)

</details>

---

## (US) TCI — `[O-WNG] [S-NG] [A] [W]` {#us-tci}

**매핑된 역할:**
- Order – WH Order Submission
- Status – Gov't & Bus
- Status – National Account
- Status – Invoice
- Warranty – Create Warranty

**가격 제한:**
- ❌ 명시된 제한 없음; 역할이 부여하는 경우 가격 권한 사용 가능

**참고 사항:**
- `U`와 같은 가격 권한은 WH Order Submission 등 특정 역할에서 제공
- `[SH-N]` 또는 `[P]` 코드가 없으므로 기본 동작 적용

---

## 모든 권한 & 가격 없음 — `[O] [S] [A] [R] [W]` {#all-permissions-no-price}

**매핑된 역할:**
- All Permissions
- No Pricing

**가격 제한:**
- ✅ `No Pricing` 역할을 통해 가격 권한 완전히 제거

**참고 사항:**
- 가격 없이 전체 접근 권한 — 조회 전용 또는 비상업적 사용자용
- `No Pricing`은 All Permissions에서 부여된 모든 `U`와 `L` 권한 제거

---

## 자동차 딜러 & 2차 공급 & 내셔널 어카운트 & 보증 {#car-dealer-secondary-supply-national-account-warranty}

**매핑된 역할:**
- Order – Car Dealer Order
- Order – Secondary Supply Submission
- National Account – Fleet Create a New Delivery Receipt
- Warranty – Create Warranty

**가격 제한:**
- ❌ 없음; 역할에 포함된 경우 가격 권한 유지

**참고 사항:**
- 전체 권한 세트를 가진 광범위한 딜러 기능 포함
- 가격 제한이 필요하다는 표시 없음

---

## 주문 제출 & 내셔널 어카운트 & 판매 보고서 {#order-submission-national-account-sales-report}

**매핑된 역할:**
- Order – WH Order Submission
- National Account – Fleet Create a New Delivery Receipt
- Report – Sales Report

**가격 제한:**
- ❌ 없음; 역할에 포함된 경우 가격 권한 유지

**참고 사항:**
- Sales Report는 `A`와 `S`만 포함 — `U` 또는 `L` 권한 없음
- Order – WH Order Submission은 `U` 포함, 따라서 제한이 없는 경우 가격 권한 사용 가능

---

## (US) 캐롤 타이어 — `[P-U] [O-SCDNG] [S-SCDNG] [W]` {#us-carroll-tire}

**매핑된 역할:**
- Order – Secondary Supply Submission
- Order – Car Dealer Order
- Order – DFC Order
- Status – Secondary Supply
- Status – Car Dealer
- Status – DFC
- Warranty – Create Warranty

**가격 제한:**
- ✅ 단가(Unit Price)만 허용 (`[P-U]`)
- ❌ 정가(List Price)는 부여되지 않음

**참고 사항:**
- 이 레거시 그룹은 부분적인 가격 접근(단가만)을 제공하도록 설계됨
- 재사용 빈도가 높다면 `Order – WH + Unit Price Only`와 같은 맞춤형 역할 생성 고려
