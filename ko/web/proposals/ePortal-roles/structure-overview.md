---
layout: default
title: RBAC 구조 개요
permalink: /ko/web/proposals/ePortal-roles/structure-overview/
nav: false
---

{% include lang-toggle.html %}

# 🧠 RBAC 구조 개요

## 개체 구조 개요

```yaml
Corporation: [국가]
└── 산업 부문: [부문]
    └── 기능: [기능]
        └── 작업 유형: [생성 | 상태]
            ├── 비즈니스 채널: [채널 1]
            │   └── 접근 수준: [A/S/U/L]
            └── 비즈니스 채널: [채널 2]
                └── 접근 수준: [A/S/U/L]
```

## 카테고리

<details markdown="1">
  <summary>🏢 법인</summary>

- US
- CA
- MX
- PA
- CO
- CL
</details>

<details markdown="1">
  <summary>🏭 산업 부문</summary>

<details markdown="1">
  <summary>도매</summary>

**기능:** 주문, 클레임, 반품, 보증 반품, 재무, 보고서
</details>

<details markdown="1">
  <summary>소매</summary>

**기능:** 주문, 클레임, 반품, 보증 반품, 재무, 보고서
</details>

<details markdown="1">
  <summary>플릿</summary>

**기능:** 주문, 클레임, 반품, 보증 반품, 재무, 보고서
</details>

<details markdown="1">
  <summary>보험</summary>

**기능:** 주문, 클레임, 반품, 보증 반품, 재무, 보고서
</details>

<details markdown="1">
  <summary>상업</summary>

**기능:** 주문, 클레임, 반품, 보증 반품, 재무, 보고서
</details>

<details markdown="1">
  <summary>도매 + 소매</summary>

**기능:** 주문, 클레임, 반품, 보증 반품, 재무, 보고서
</details>
</details>

<details markdown="1">
  <summary>📁 기능</summary>

<details markdown="1">
  <summary>주문</summary>

**작업:** 생성, 상태
</details>

<details markdown="1">
  <summary>클레임</summary>

**작업:** 생성, 상태
</details>

<details markdown="1">
  <summary>반품</summary>

**작업:** 생성, 상태
</details>

<details markdown="1">
  <summary>보증 반품</summary>

**작업:** 생성, 상태
</details>

<details markdown="1">
  <summary>재무</summary>

**작업:** 생성, 상태
</details>

<details markdown="1">
  <summary>보고서</summary>

**작업:** 생성, 상태
</details>
</details>

<details markdown="1">
  <summary>🎯 작업 유형</summary>

- 생성
- 상태
</details>

<details markdown="1">
  <summary>🧭 비즈니스 채널</summary>

- WH (창고)
- SSP (보조 공급)
- CDTP (자동차 딜러)
- DFC
- NAP (전국 계정 프로그램)
- 정부 &amp; 사업
</details>

<details markdown="1">
  <summary>🔐 접근 수준</summary>

- 접근 (A)
- 재고 (S)
- 단가 (U)
- 정가 (L)
</details>

## 🧪 예시

```yaml
Corporation: US
└── 산업 부문: 플릿
    └── 기능: 주문
        └── 작업 유형: 생성
            ├── 비즈니스 채널: WH
            │   └── 접근 수준: A, S, U
            └── 비즈니스 채널: DFC
                └── 접근 수준: A
```

```yaml
Corporation: US
    ├── 산업 부문: 플릿
    │   ├── 기능: 주문
    │   │   ├── 작업 유형: 생성
    │   │   │   ├── 비즈니스 채널: WH
    │   │   │   │   └── 접근 수준: A, S, U
    │   │   │   └── 비즈니스 채널: DFC
    │   │   │       └── 접근 수준: A
    │   │   └── 작업 유형: 상태
    │   │       └── 비즈니스 채널: WH
    │   │           └── 접근 수준: A, S
    │   ├── 기능: 보증 반품
    │   │   ├── 작업 유형: 생성
    │   │   │   └── 비즈니스 채널: WH
    │   │   │       └── 접근 수준: A, S
    │   │   └── 작업 유형: 상태
    │   │       └── 비즈니스 채널: WH
    │   │           └── 접근 수준: A, S
    │   └── 기능: 보고서
    │       └── 작업 유형: 상태
    │           ├── 비즈니스 채널: 판매 보고서
    │           │   └── 접근 수준: A, S
    │           └── 비즈니스 채널: 재고 보고서
    │               └── 접근 수준: A, S
    └── 산업 부문: 소매
        ├── 기능: 주문
        │   ├── 작업 유형: 생성
        │   │   ├── 비즈니스 채널: SSP
        │   │   │   └── 접근 수준: A
        │   │   └── 비즈니스 채널: CDTP
        │   │       └── 접근 수준: A, S, U
        │   └── 작업 유형: 상태
        │       └── 비즈니스 채널: CDTP
        │           └── 접근 수준: A
        └── 기능: 보고서
            └── 작업 유형: 상태
                └── 비즈니스 채널: 명세서
                    └── 접근 수준: A
```