---
layout: default
title: 직접 권한 부여
permalink: /ko/web/proposals/ePortal-roles/direct-privileges/
nav: false
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">
{% include lang-toggle.html %}

# 🧩 직접 권한 부여

이 문서는 사용자가 할당된 역할 외에 개별 권한 및 권한 수준(Privileges) 재정의를 직접 적용하는 방법을 설명합니다.  
직접 권한 부여는 `No Pricing`과 같은 필터나 역할로는 충분하지 않을 때에만 **드물게** 사용해야 합니다.

---

<details markdown="1">
  <summary><strong>📑 목차 (클릭하여 펼치기)</strong></summary>

- [`직접 권한 부여를 사용하는 경우`](#직접-권한-부여를-사용하는-경우)
- [`직접 권한 부여의 동작 방식`](#직접-권한-부여의-동작-방식)
- [`예시`](#예시)
- [`모범 사례`](#모범-사례)

</details>

---

## 직접 권한 부여를 사용하는 경우

다음과 같은 경우 직접 권한 부여를 사용합니다:

- **추가 권한이나 권한 수준** 하나만 필요한 경우
- 특정 상황에서 **`No Pricing` 역할을 무시**해야 하는 경우
- 재사용 가능한 역할로 만들 가치가 없는 **드문 조합**이 필요한 경우

---

## 직접 권한 부여의 동작 방식

직접 권한 부여는 사용자의 역할과 별도로 저장됩니다. 이를 통해:

- 특정 권한에 대해 특정 권한 수준(`A`, `S`, `U`, `L`)을 추가 또는 재정의할 수 있습니다.
- 상속된 역할 기반 권한을 보완하거나 재정의할 수 있습니다.

`No Pricing`과 같은 역할 및 필터 **적용 이후**에 평가됩니다.

---

## 예시

### ✅ 예시 1: Sales Report에만 단가(Unit Price) 추가

**사용자 역할:**

- `Report – Sales Report` ( `A`, `S` 권한 부여)
- `No Pricing` (`U`, `L` 제거)

→ **직접 권한 부여 추가:**
```text
사용자: jdoe
권한: Report → Sales Report
권한 수준: U
```

**결과:**

- 역할에서 `A`, `S`  
- 직접 권한 부여에서 `U`  
- `L`은 여전히 `No Pricing`으로 인해 제거됨  

---

### ✅ 예시 2: 맞춤형 인보이스 접근

사용자는 `Invoice` 역할이 필요하지 않고, 재고 수준 인보이스 데이터만 보고 싶어함.

→ **직접 권한 부여 추가:**
```text
사용자: jsmith
권한: Status → Invoice
권한 수준: A, S
```

---

## 모범 사례

- ✅ **드문 예외**에만 직접 권한 부여 사용
- ❌ 역할을 직접 권한 부여로 대체하지 않기
- 🔐 직접 권한 부여는 항상 기록하고 정기적으로 검토
- 🔄 여러 사용자가 동일한 재정의를 필요로 한다면, 역할을 업데이트하거나 작은 맞춤형 역할 생성 고려

---

표준 권한 및 권한 수준 노출에 대해서는 다음을 참조하세요:

- [role-definitions](./role-definitions.md)
- [privilege-matrix](./privilege-matrix.md)
