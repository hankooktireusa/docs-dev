---
layout: default
title: 마이그레이션 계획
permalink: /ko/web/proposals/ePortal-roles/migration-plan/
nav: false
---

{% include lang-toggle.html %}

# 🔄 역할 온보딩 계획: 새로운 RBAC 구현

이 계획은 새로운 플랫폼에서 역할 기반 접근 제어(RBAC) 시스템을 롤아웃하는 방법을 설명합니다.  
새 구조는 레거시 시스템에서 사용자가 가졌던 동일한 접근 패턴을 유지하면서도, 더 깔끔하고 표준화되며 유지 관리가 쉬운 모델을 제공합니다.

---

<details markdown="1">
  <summary><strong>📑 목차 (클릭하여 펼치기)</strong></summary>

- [`📌 1단계: 접근 패턴 분석`](#phase-1-access-pattern-analysis)
- [`📌 2단계: 역할 설계 확정`](#phase-2-role-design-finalization)
- [`📌 3단계: 초기 사용자 역할 할당`](#phase-3-initial-user-role-assignment)
- [`📌 4단계: 테스트 및 검증`](#phase-4-testing--verification)
- [`📌 5단계: 운영 배포`](#phase-5-production-deployment)
- [`🧩 참고 사항`](#notes)

</details>

---

## 📌 1단계: 접근 패턴 분석 {#phase-1-access-pattern-analysis}

*목표:* 새 사이트의 모든 사용자 유형에 필요한 접근 패턴과 권한 세트를 식별합니다.

**✅ 단계:**
1. **사용자 페르소나와 비즈니스 기능 정의**
2. **필요한 모든 권한과 해당 권한 수준 나열**
3. **공통 조합을 잠재적인 역할에 매핑**
4. **특수 또는 제한 시나리오 문서화** (예: No Pricing)

---

## 📌 2단계: 역할 설계 확정 {#phase-2-role-design-finalization}

*목표:* 모든 표준 접근 요구사항을 반영하는 [role-definitions](./role-definitions.md) 내의 깔끔한 역할 세트를 구축합니다.

**✅ 단계:**
1. **기본 역할 정의** (예: 주문 제출자, 플릿 뷰어)
2. **범위 지정 로직 포함** (예: 지역, 세그먼트)
3. `No Pricing` 또는 `Report Only`와 같은 수정자 역할 추가
4. 역할 커버리지가 모든 문서화된 접근 요구사항을 충족하는지 확인

---

## 📌 3단계: 초기 사용자 역할 할당 {#phase-3-initial-user-role-assignment}

*목표:* 새 플랫폼에서의 예상 사용 사례를 기반으로 사용자를 역할에 할당합니다.

**✅ 단계:**
1. 페르소나에 따라 사용자별로 하나 이상의 역할 할당
2. 해당되는 경우 범위 지정 역할 사용 (예: Fleet CA 전용)
3. 필요 시 제한적 역할 적용 (예: `No Pricing`)
4. 예외 케이스에 대한 직접 권한 재정의 문서화

---

## 📌 4단계: 테스트 및 검증 {#phase-4-testing--verification}

*목표:* 모든 역할이 의도된 접근을 제공하고 제한이 올바르게 작동하는지 확인합니다.

**✅ 단계:**
1. 샘플 사용자에 대해 모든 기본 역할 테스트
2. 다양한 맥락에서 범위 지정 동작 검증
3. 제한적 역할(`No Pricing` 등)의 동작 확인
4. 예기치 않은 접근 누락 또는 과도한 권한 문제를 기록하고 해결

---

## 📌 5단계: 운영 배포 {#phase-5-production-deployment}

*목표:* 새로운 플랫폼에서 RBAC 시스템을 깨끗한 추적 및 관측 가능성과 함께 출시합니다.

**✅ 단계:**
1. 새 사이트에서 역할 기반 접근 제어 활성화
2. 사용자 유형별 활동 및 동작 모니터링
3. 피드백 또는 예외적 접근 문제를 추적 및 해결
4. 정기적인 접근 검토 계획 수립

---

## 🧩 참고 사항 {#notes}

- 이 RBAC 모델은 레거시 시스템에서 사용자가 가졌던 동일한 접근 수준을 지원하면서, **더 구조적이고 유지 관리가 용이하며 투명한 접근 방식**을 제공합니다.
- `All Permissions` 역할은 관리자 또는 전체 접근이 필요한 경우 사용할 수 있습니다.
- `No Pricing`과 같은 제한적 역할은 전역 접근 제어를 제공합니다.
- 직접 권한 재정의는 지원되지만, 드물게 사용해야 하며 반드시 기록해야 합니다.
