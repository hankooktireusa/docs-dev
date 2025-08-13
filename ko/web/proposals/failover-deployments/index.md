---
layout: default
title: "📑 페일오버 배포"
lang: ko
permalink: /ko/web/proposals/failover-deployments/
---

{% include lang-toggle.html %}

# 📑 페일오버 배포

가중치 기반 ALB(Target Group) 라우팅을 사용해 **prod1 ↔ prod2** 무중단 전환을 구현합니다.

---

## 🎯 목표

- 배포 중에는 트래픽을 **prod1**에 100% 보내고 **prod2**에 배포합니다.
- 이후 트래픽을 **prod2**로 단계적으로 전환합니다(예: 10% → 25% → 50% → 100%).
- 다음 배포 사이클에서는 역할을 바꿔 **prod2**를 라이브로 두고 **prod1**에 배포합니다.
- 검증 완료 후에는 균등 분배로 복귀합니다.
- ALB 리스너의 포워딩 동작을 **Weighted Target Groups**로 전환하여 구현합니다.

---

<details>
  <summary>🛠 단계별 진행 (AWS 콘솔)</summary>
  <div markdown="1">

### 1) 현재 리스너 규칙 점검
- AWS Console → **EC2 → Load Balancers**
- 대상 **ALB** 선택 → **Listeners** 탭 → **:443** 클릭
- 호스트/경로 매칭 규칙이 `-web-tg` 또는 `-portal-tg`로 포워딩되는지 확인

---

### 2) 고정 포워딩 → 가중치 기반(Target Groups) 전환
**목표:** prod1 / prod2 두 타깃 그룹으로 가중치를 조절하며 포워딩

**예시 타깃 그룹:**
- `hankooktire-us-prd-<web|portal>-01-tg` (prod1)
- `hankooktire-us-prd-<web|portal>-02-tg` (prod2)

**방법:**
1. 해당 규칙을 **Edit**.
2. **Forward to → Weighted target groups** 선택.
3. 두 타깃 그룹을 추가하고 초기 가중치 설정:
   - `...-01-tg` → **100**
   - `...-02-tg` → **0**
4. 저장.

---

### 3) prod1 100% 상태 검증
- HTTPS 트래픽이 모두 **prod1**으로 전달되는지 확인.
- **prod2**는 유휴 상태이므로 안전하게 배포 가능.
- prod2(`...-02-tg` 인스턴스)에 배포 진행.

---

### 4) prod2로 단계적 전환
1. 해당 리스너 규칙으로 이동.
2. 각 단계별로 가중치를 조절하며 테스트:
   - 90/10 → 75/25 → 50/50 → 25/75 → 0/100 (또는 팀 내 합의된 단계)
3. 각 단계에서 애플리케이션 동작 검증.
4. **CloudWatch** 지표(TG Health, 지연, 4xx/5xx) 모니터링.

---

### 5) 다음 배포 사이클에서 역할 전환
1. **prod1 TG** 가중치를 **0**으로 설정.
2. 배포.
3. 다시 **100**까지 램프업.
4. 모니터링/테스트 후 최종 확정.

  </div>
</details>

---

<details>
  <summary>📌 참고 사항</summary>
  <div markdown="1">

- 추가적인 AWS 서비스 도입이나 비용 증가는 없습니다.
- 무중단 전환: 가중치 `0`은 **새로운** 연결만 차단하고, 기존 연결은 정상 종료를 허용합니다.
- 타깃 그룹 **스티키니스(stickiness)** 는 **비활성화**되어 있어 램프업 중 세션이 기존 TG에 묶이지 않습니다.
- 기존 배포 프로세스는 변경하지 않습니다.
- 페일오버 배포 시 팀과 사전 공조가 필요합니다.
- 현재 **Dev ALB**는 동일 구성을 사용하지 않을 수 있습니다:
  - 모범 사례: **dev** 환경에도 가중치 규칙을 복제하고 선(先) 검증 후 운영에 적용하세요.

  </div>
</details>
