---
layout: default
title: 장애 조치 배포
permalink: /ko/web/proposals/failover-deployments/
nav: false
---

{% include lang-toggle.html %}

# 장애 조치 배포

가중치가 있는 ALB(Target Group) 라우팅을 통해 **prod1 ↔ prod2** 사이의 무중단 전환을 구현합니다.

---

## 목표
- 배포 중에는 트래픽을 **prod1**에 100% 보내고, **prod2**에는 배포를 수행합니다.
- 배포 후 **prod2**로 트래픽을 단계적으로 전환합니다(예: 90/10 → 75/25 → 50/50 → 25/75 → 0/100).
- 다음 배포 사이클에서는 역할을 뒤집습니다(**prod2** 운영, **prod1**에 배포).
- 검증이 끝나면 균등 분배로 복귀합니다.
- ALB의 Listener 전달 동작을 **Weighted Target Groups**로 전환하여 달성합니다.

---

<details markdown="1">
  <summary>단계별 계획 (AWS 콘솔)</summary>

### 1) 현재 Listener 규칙 확인
- AWS 콘솔 → **EC2 → Load Balancers**
- 대상 **ALB** 선택 → **Listeners** 탭 → **:443** 클릭
- 호스트/경로 매칭 후 `-web-tg` 또는 `-portal-tg`로 전달하는 규칙을 확인합니다.

---

### 2) 고정 전달 규칙 → 가중치 대상 그룹으로 전환
**목표:** 조절 가능한 가중치로 prod1 & prod2 **두 대상 그룹**에 전달합니다.

**예시 대상 그룹:**
- `hankooktire-us-prd-<web|portal>-01-tg` (prod1)
- `hankooktire-us-prd-<web|portal>-02-tg` (prod2)

**방법:**
1. 해당 규칙을 **Edit** 합니다.
2. **Forward to → Weighted target groups** 를 선택합니다.
3. 두 대상 그룹을 추가하고 초기 가중치를 설정합니다:
   - `…-01-tg` → **100**
   - `…-02-tg` → **0**
4. **Save** 합니다.

---

### 3) prod1에 100% 전달 검증
- 모든 HTTPS 트래픽이 **prod1**으로 전달되는지 확인합니다.
- **prod2**는 유휴 상태이므로 배포에 안전합니다.
- **prod2**(`…-02-tg` 인스턴스)에 배포합니다.

---

### 4) prod2로 단계적 트래픽 전환
1. Listener 규칙으로 돌아갑니다.
2. 각 단계마다 테스트하며 가중치를 조정합니다:
   - 90/10 → 75/25 → 50/50 → 25/75 → 0/100 (또는 팀에서 정한 단계)
3. 각 단계에서 애플리케이션 동작을 검증합니다.
4. **CloudWatch** 지표(TG 헬스, 지연 시간, 4xx/5xx)를 모니터링합니다.

---

### 5) 다음 배포를 위한 역할 전환
1. **prod1 TG** 가중치를 **0**으로 설정합니다.
2. 배포를 수행합니다.
3. 다시 **100**으로 램프업합니다.
4. 모니터링/테스트 후 최종 확정합니다.

</details>

---

<details markdown="1">
  <summary>참고 사항</summary>

- 추가 AWS 서비스나 비용 변경은 없습니다.
- 무중단 접근 방식: 가중치 **0**은 **새로운** 연결만 차단하고, 기존 연결은 완료됩니다.
- TG **stickiness는 비활성화**되어 있어 전환 중 이전 TG에 세션이 붙지 않습니다.
- 상위 배포 프로세스는 변경되지 않습니다.
- 장애 조치 배포 시 팀과 일정/단계를 사전에 조율하세요.
- 현재 **Dev ALB**는 동일 구성을 반영하지 않습니다:
  - 모범 사례: **dev**에서 가중치 규칙을 복제해 먼저 리허설하세요.

</details>

---

<details markdown="1">
  <summary>확장: 디버그 / 렌더링 확인</summary>

스타일과 마크다운 처리를 모니터링하기 위한 임시 접기 영역입니다.

```bash
echo "Hello from /ko/web/proposals/failover-deployments/index.md within collapsible"
ls -la
```
</details>

### 렌더링 확인 (접기 기능 외부)

```bash
echo "Hello from /ko/web/proposals/failover-deployments/index.md outside collapsible"
```
