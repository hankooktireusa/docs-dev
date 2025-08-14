---
layout: default
title: 역할 정의
permalink: /ko/web/proposals/ePortal-roles/role-definitions/
nav: false
---

{% include lang-toggle.html %}

# 📘 역할 정의

**ℹ️ 이 역할 카탈로그는 새로운 RBAC 모델을 반영합니다.**  
본 문서의 각 역할은 기존 그룹 사용 패턴을 참고하되, 깔끔하고 일관성 있으며 재사용 가능한 접근 번들을 만들기 위해 리팩토링되었습니다.  
역할은 기본적으로 최소 권한(Least Privilege) 원칙에 따라 설계되며, 필요한 경우에만 예외 권한이 적용됩니다.

---

<details markdown="1">
  <summary><strong>📑 목차 (클릭하여 펼치기)</strong></summary>

- [`주문 – WH 주문 제출`](#order--wh-order-submission)
- [`주문 – WH 퀵 오더`](#order--wh-quick-order)
- [`주문 – 2차 공급 배송 조회`](#order--secondary-supply-delivery-check)
- [`주문 – 2차 공급 주문 제출`](#order--secondary-supply-submission)
- [`주문 – 카딜러 주문`](#order--car-dealer-order)
- [`주문 – DFC 주문`](#order--dfc-order)
- [`내셔널 어카운트 – 플릿 신규 배송 전표 생성`](#national-account--fleet-create-a-new-delivery-receipt)
- [`내셔널 어카운트 – Gov't & Bus`](#national-account--govt--bus)
- [`상태 – 주문 제출`](#status--order-submission)
- [`상태 – 2차 공급`](#status--secondary-supply)
- [`상태 – Gov't & Bus`](#status--govt--bus)
- [`상태 – 카딜러`](#status--car-dealer)
- [`상태 – DFC`](#status--dfc)
- [`상태 – 미결 항목`](#status--open-items)
- [`상태 – 송장`](#status--invoice)
- [`보고서 – 명세서`](#report--statement)
- [`보고서 – 판매 보고서`](#report--sales-report)
- [`보고서 – 재고 보고서`](#report--stock-report)
- [`보증 – 보증 생성`](#warranty--create-warranty)
- [`보증 – 보증 상태`](#warranty--warranty-status)
- [`모든 권한`](#all-permissions)

</details>

---

## `주문 – WH 주문 제출` {#order--wh-order-submission}

창고 기반 주문 제출 기능을 부여합니다.  
**권한:** 주문 → WH 주문 제출: A, S, U  
**참고:** 종종 상태/보고서 역할과 함께 사용되며, 가격 제한이 필요한 경우 *No Pricing*을 추가합니다.

---

## `주문 – WH 퀵 오더` {#order--wh-quick-order}

창고 시스템에서 빠른 주문 입력 기능을 제공합니다.  
**권한:** 주문 → WH 퀵 오더: A, S, U

---

## `주문 – 2차 공급 배송 조회` {#order--secondary-supply-delivery-check}

2차 공급에서 재고/배송 가능 여부를 조회합니다.  
**권한:** 주문 → 2차 공급 → 배송 조회: A

---

## `주문 – 2차 공급 주문 제출` {#order--secondary-supply-submission}

2차 공급 네트워크를 통해 주문을 제출합니다.  
**권한:** 주문 → 2차 공급 → 주문 제출: A, S, U

---

## `주문 – 카딜러 주문` {#order--car-dealer-order}

카딜러 주문을 직접 제출합니다.  
**권한:** 주문 → 카딜러 → 주문: A, S, U

---

## `주문 – DFC 주문` {#order--dfc-order}

직접 물류 센터 주문을 제출합니다.  
**권한:** 주문 → DFC 주문: A

---

## `내셔널 어카운트 – 플릿 신규 배송 전표 생성` {#national-account--fleet-create-a-new-delivery-receipt}

플릿 계정을 위한 배송 전표를 생성합니다.  
**권한:** Hankook National Fleets → 신규 배송 전표 생성: A

---

## `내셔널 어카운트 – Gov't & Bus` {#national-account--govt--bus}

내셔널 어카운트를 통한 정부/비즈니스 채널 작업을 수행합니다.  
**권한:** Gov’t & Bus: A

---

## `상태 – 주문 제출` {#status--order-submission}

제출된 주문 상태를 조회합니다.  
**권한:** 상태 → 주문 제출: A, S, U

---

## `상태 – 2차 공급` {#status--secondary-supply}

2차 공급 주문을 추적합니다.  
**권한:** 상태 → 2차 공급: A, S, U

---

## `상태 – Gov't & Bus` {#status--govt--bus}

정부/비즈니스 주문 상태를 조회합니다.  
**권한:** 상태 → Gov’t & Bus: A

---

## `상태 – 카딜러` {#status--car-dealer}

카딜러 주문을 추적합니다.  
**권한:** 상태 → 카딜러: A

---

## `상태 – DFC` {#status--dfc}

직접 물류 센터 주문을 추적합니다.  
**권한:** 상태 → DFC: A

---

## `상태 – 미결 항목` {#status--open-items}

미지급/미처리 청구 항목을 조회합니다.  
**권한:** 상태 → 미결 항목: A

---

## `상태 – 송장` {#status--invoice}

송장과 재고 세부 정보를 조회합니다.  
**권한:** 상태 → 송장: A, S

---

## `보고서 – 명세서` {#report--statement}

계정 재무 명세서를 조회합니다.  
**권한:** 보고서 → 명세서: A

---

## `보고서 – 판매 보고서` {#report--sales-report}

판매 지표를 조회합니다.  
**권한:** 보고서 → 판매 보고서: A, S

---

## `보고서 – 재고 보고서` {#report--stock-report}

현재 재고를 조회합니다.  
**권한:** 보고서 → 재고 보고서: A, S

---

## `보증 – 보증 생성` {#warranty--create-warranty}

신규 보증 청구를 제출합니다.  
**권한:** 보증 반환 → 생성: A, S

---

## `보증 – 보증 상태` {#warranty--warranty-status}

보증 청구 상태를 조회합니다.  
**권한:** 보증 반환 → 상태: A, S

---

## `모든 권한` {#all-permissions}

가격, 보고서, 주문, 보증 등 전체 시스템 접근 권한을 부여합니다.  
**권한:** 모든 정의된 권한: A, S, U, L  
**참고:** 관리자 전용; 기본적으로 부여하지 않습니다.
