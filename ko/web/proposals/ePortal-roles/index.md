---
layout: default
title: "🧠 역할 & 권한 문서"
lang: ko
permalink: /ko/web/proposals/ePortal-roles/
---

{% include lang-toggle.html %}

# 🧠 역할 & 권한 문서

이 프로젝트는 복잡한 레거시 그룹을 **유지보수하기 쉬운 역할·권한 체계(RBAC)** 로 정리합니다.  
예외 케이스, 가격 제한, 사용자별 직접 오버라이드도 지원하며, 레거시와 **동등한 접근 수준**을 보장합니다.

---

## 📑 목차

- 🧠 [역할 & 권한 개요]({{ '/ko/web/proposals/ePortal-roles/structure-overview/' | relative_url }})  
  _역할 범주, 기능, 액션, 비즈니스 채널, 접근 레벨의 시각적 구조._

- 📊 [RBAC 데이터 모델]({{ '/ko/web/proposals/ePortal-roles/data-model/' | relative_url }})  
  _역할·권한 구조의 핵심 테이블과 관계._

- 🧱 [테이블 정의]({{ '/ko/web/proposals/ePortal-roles/table-definitions/' | relative_url }})  
  _각 테이블의 컬럼, 관계, 비고를 상세 기술._

- 🧩 [역할 정의]({{ '/ko/web/proposals/ePortal-roles/role-definitions/' | relative_url }})  
  _모든 기본 역할과 부여된 권한 목록._

- 🔄 [마이그레이션 계획]({{ '/ko/web/proposals/ePortal-roles/migration-plan/' | relative_url }})  
  _레거시 그룹을 RBAC 역할로 전환하고 배포하는 단계별 절차._

- 🧮 [권한 매트릭스]({{ '/ko/web/proposals/ePortal-roles/privilege-matrix/' | relative_url }})  
  _레거시 권한을 신규 권한으로 매핑._

- 🧭 [평가 순서]({{ '/ko/web/proposals/ePortal-roles/evaluation-order/' | relative_url }})  
  _겹치는 권한을 우선순위로 해소하는 규칙._

- 🚫 [가격 노출 금지 규칙]({{ '/ko/web/proposals/ePortal-roles/no-pricing-rules/' | relative_url }})  
  _특정 조건에서 가격 권한을 제거하는 제한 규칙._

- 🧾 [레거시 매핑]({{ '/ko/web/proposals/ePortal-roles/legacy-mapping/' | relative_url }})  
  _레거시 그룹을 현대적 역할로 해석하는 방법._

- 🧷 [직접 권한]({{ '/ko/web/proposals/ePortal-roles/direct-privileges/' | relative_url }})  
  _역할 상속 외 사용자별 예외 권한 부여 가이드._
