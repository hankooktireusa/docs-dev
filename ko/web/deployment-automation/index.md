---
layout: default
title: 배포
permalink: /ko/web/deployment-automation/
nav: true
---

{% include lang-toggle.html %}

# 배포 자동화

이 프로젝트는 **CustomerPortal (CP)** 과 **WebOrder (WO)** 를 DEV 및 PROD 환경에 배포하는 과정을 PowerShell, WinSCP, PuTTY로 자동화합니다.

---

## 스크립트 다운로드

1. [ZIP 다운로드]({{ '/assets/downloads/deployment-automation-scripts.zip' | relative_url }})
2. 아래 경로에 압축 해제:
   ```text
   C:\scripts\deployment-automation
   ```
3. PowerShell에서 실행:
   ```powershell
   .\main.ps1
   ```

자세한 설정 및 구성은 ZIP 내부의 **README.md** 를 확인하세요.

---

## 주요 기능
- 환경 인지형 설정 전환(데이터소스, SAP, WSDL)
- 선택적 Maven 빌드 단계
- WinSCP를 통한 안전한 WAR/ROOT 백업 및 전송
- PuTTY 및 WinSCP용 SSH 호스트 키 신뢰 자동화
- PuTTY 자동화를 통한 Tomcat 재시작 및 실시간 로그 모니터링
- 동일 WAR 파일로 **PROD1 → PROD2** 연속 배포
- 배포 후 확인, 롤백 및 정리 지원

---

## 스크립트 구성(ZIP 포함)
```yaml
deployment-automation/
├── config.ps1                           # 공통 경로, 세션명, SSH 호스트 키
├── main.ps1                             # 전체 배포 자동화 진입점
├── README.md                            # 사용 가이드와 설정 안내
│
├── lib/
│   ├── git.ps1
│   ├── maven.ps1
│   ├── post-check-prompts.ps1
│   ├── post-check-and-rollback.ps1
│   ├── putty-automation.ps1
│   ├── putty.ps1
│   ├── rollback-deployment.ps1
│   ├── verify-war-file.ps1
│   ├── winscp-deploy.ps1
│   └── deploy-to-second-prod.ps1
│
└── switch-env-servers/
    ├── switch-datasource-server.ps1
    ├── switch-sap-properties.ps1
    └── switch-wsdl-info.ps1
```

---

## 배포 흐름 개요
```
          ┌───────────────┐
          │   앱 선택     │
          └───────┬───────┘
                  ▼
           ┌──────▼──────┐
           │  환경 선택  │
           └──────┬──────┘
                  ▼
      ┌───────────▼────────────┐
      │       Git Pull         │  ← PROD2 연속 배포 시 생략
      └───────────┬────────────┘
                  ▼
         ┌────────▼────────┐
         │   설정 전환     │
         └────────┬────────┘
                  ▼
        ┌─────────▼─────────┐
        │ Maven 빌드 실행   │
        └─────────┬─────────┘
                  ▼
        ┌─────────▼──────────┐
        │  WAR 파일 검증     │
        └─────────┬──────────┘
                  ▼
     ┌────────────▼─────────────┐
     │  PuTTY 세션 시작         │
     └────────────┬─────────────┘
                  ▼
   ┌──────────────▼──────────────┐
   │ WinSCP로 WAR 전송           │
   └──────────────┬──────────────┘
                  ▼
  ┌───────────────▼────────────────┐
  │ 기존 WAR → 백업 이름 변경      │
  │ 새 WAR를 ROOT.war로 배포       │
  └───────────────┬────────────────┘
                  ▼
     ┌────────────▼─────────────┐
     │ PuTTY로 Tomcat 재시작    │
     └────────────┬─────────────┘
                  ▼
     ┌────────────▼────────────┐
     │ 로그 확인 + 롤백 여부   │
     └────────────┬────────────┘
                  ▼
         ┌────────▼────────┐
         │  PROD2에 배포?  │
         └────────┬────────┘
                  ▼ 예
      (다시: PuTTY 세션 → WAR 업로드 → 재시작)
                  ▼
     ┌────────────▼──────────────┐
     │ 설정을 LOCAL로 복원       │
     │ 열린 PuTTY 세션 종료      │
     └───────────────────────────┘
```

---

## 신규 개발자를 위한 안내
이 도구는 CP/WO 전체 배포 흐름을 프롬프트, 검증, 안전한 롤백과 함께 단계별로 안내합니다. 첫 실행 시에는 동료와 함께 진행해 보세요.

---

<details markdown="1">
  <summary>확장: 디버그 / 렌더링 확인</summary>

스타일과 마크다운 처리를 모니터링하기 위한 임시 접기 영역입니다.

```bash
echo "Hello from /ko/web/deployment-automation/index.md within collapsible"
ls -la
```
</details>

### 렌더링 확인 (접기 기능 외부)

```bash
echo "Hello from /ko/web/deployment-automation/index.md outside collapsible"
```
