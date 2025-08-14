---
layout: default
title: ePortal 역할
permalink: /ko/web/proposals/ePortal-roles/
nav: false
---

{% include lang-toggle.html %}

# 역할 & 권한 문서

이 프로젝트는 복잡한 레거시 그룹을 **역할 기반 접근 제어(RBAC)** 로 단순화하여 유지보수 가능한 역할과 권한 체계를 제공합니다. 가격 제한, 직접 오버라이드 같은 예외 상황도 지원하면서 레거시 시스템의 동등한 접근 수준을 보존합니다.

---

## 목차
- [역할 & 권한 개요](./structure-overview/)  
  *역할 카테고리, 기능, 액션, 채널, 접근 레벨을 시각적으로 정리합니다.*
- [RBAC 데이터 모델](./data-model/)  
  *새 역할/권한 구조의 핵심 테이블과 관계를 설명합니다.*
- [테이블 정의](./table-definitions/)  
  *각 테이블의 컬럼, 관계, 비고를 상세히 기술합니다.*
- [역할 정의](./role-definitions/)  
  *모든 기본 역할과 할당된 권한을 정리합니다.*
- [마이그레이션 계획](./migration-plan/)  
  *레거시 그룹을 RBAC 역할로 전환하고 배포하는 절차를 단계별로 설명합니다.*
- [권한 매트릭스](./privilege-matrix/)  
  *레거시 권한을 새 권한에 매핑합니다.*
- [평가 순서](./evaluation-order/)  
  *중복/충돌 권한의 우선순위 해소 과정을 명확히 합니다.*
- [가격 미표시 규칙](./no-pricing-rules/)  
  *특정 예외 상황에서 가격 권한을 제거하는 제한 규칙을 정의합니다.*
- [레거시 매핑](./legacy-mapping/)  
  *레거시 그룹을 현대적 역할로 해석/전환하는 방법을 문서화합니다.*
- [직접 권한](./direct-privileges/)  
  *역할 상속과 별도로 사용자 단위 오버라이드를 부여하는 가이던스입니다.*

---

<details markdown="1">
  <summary>확장: 디버그 / 렌더링 확인</summary>

스타일과 마크다운 처리를 모니터링하기 위한 임시 접기 영역입니다.

```bash
echo "Hello from /ko/web/proposals/ePortal-roles/index.md within collapsible"
ls -la
```
</details>

### 렌더링 확인 (접기 기능 외부)

```bash
echo "Hello from /ko/web/proposals/ePortal-roles/index.md outside collapsible"
```
