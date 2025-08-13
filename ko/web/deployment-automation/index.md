---
layout: default
title: "⚙️ CustomerPortal (CP) 및 WebOrder (WO) 배포 자동화"
lang: ko
permalink: /ko/web/deployment-automation/
---

{% include lang-toggle.html %}

# ⚙️ CustomerPortal (CP) 및 WebOrder (WO) 배포 자동화

이 프로젝트는 **CustomerPortal (CP)** 과 **WebOrder (WO)** 애플리케이션을 DEV/PROD 환경에 배포하는 작업을 PowerShell, WinSCP, PuTTY로 자동화합니다.

---

## 📥 스크립트 다운로드

로컬에서 배포 자동화를 실행하려면:

1. [⬇️ deployment-automation-scripts.zip 내려받기]({{ '/assets/downloads/deployment-automation-scripts.zip' | relative_url }})
2. 다음 경로에 압축 해제:
    C:\scripts\deployment-automation
3. PowerShell에서 실행:
~~~powershell
.\main.ps1
~~~

전체 설정 및 사용 방법은 ZIP 묶음 안의 **README.md**를 참고하세요.

> ZIP 파일 위치: `assets/downloads/deployment-automation-scripts.zip` (루트 공유 에셋 — EN/KO에서 공용으로 사용)

---

## ✨ 특징

- 🔄 환경 인지형 구성 전환(데이터소스, SAP, WSDL)
- ⚙️ 선택적 Maven 빌드 단계
- 📦 WinSCP를 통한 안전한 WAR/ROOT 백업 및 전송
- 🔐 PuTTY 및 WinSCP용 동적 SSH 호스트 키 신뢰
- 🖥️ Tomcat 재시작 및 실시간 로그 모니터링 자동화
- 🔁 동일한 WAR로 **PROD1 → PROD2** 연속 배포
- ⏪ 배포 후 확인, 롤백 및 정리 지원

---

## 📁 스크립트 구조 (ZIP 포함)
~~~yaml
deployment-automation/
├── config.ps1                           # 공통 경로, 세션명, SSH 호스트 키
├── main.ps1                             # 전체 배포 자동화 진입점
├── README.md                            # 전체 사용 가이드 및 설정 안내
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
~~~

---

## 🧭 배포 흐름 개요
~~~
          ┌───────────────┐
          │  Select App   │
          └───────┬───────┘
                  ▼
           ┌──────▼──────┐
           │ Select Env  │
           └──────┬──────┘
                  ▼
      ┌───────────▼────────────┐
      │      Git Pull          │  ← Skipped on PROD2 continuation
      └───────────┬────────────┘
                  ▼
         ┌────────▼────────┐
         │  Config Switch  │
         └────────┬────────┘
                  ▼
        ┌─────────▼─────────┐
        │ Run Maven Build   │
        └─────────┬─────────┘
                  ▼
        ┌─────────▼──────────┐
        │ Validate WAR File  │
        └─────────┬──────────┘
                  ▼
     ┌────────────▼─────────────┐
     │  Start PuTTY Sessions    │
     └────────────┬─────────────┘
                  ▼
   ┌──────────────▼──────────────┐
   │ Transfer WAR using WinSCP   │
   └──────────────┬──────────────┘
                  ▼
  ┌───────────────▼────────────────┐
  │ Rename existing WAR → backup   │
  │ Deploy new WAR as ROOT.war     │
  └───────────────┬────────────────┘
                  ▼
     ┌────────────▼─────────────┐
     │ Restart Tomcat via PuTTY │
     └────────────┬─────────────┘
                  ▼
     ┌────────────▼────────────┐
     │ Check Logs + Rollback?  │
     └────────────┬────────────┘
                  ▼
         ┌────────▼────────┐
         │ Deploy to PROD2?│
         └────────┬────────┘
                  ▼ Yes
      (Resume from: PuTTY session → WAR upload → restart)
                  ▼
     ┌────────────▼──────────────┐
     │ Revert Configs to LOCAL   │
     │ Close open PuTTY sessions │
     └───────────────────────────┘
~~~

---

## 👥 신규 개발자 안내

이 도구는 CP/WO 프로젝트의 전체 배포 흐름을 단계별로 안내합니다. 각 단계에서 확인/검증과 안전한 롤백 절차를 제공하므로, 화면의 지시에 따라 진행하면 됩니다.

첫 실행 시 팀 동료와 함께 진행해 보세요!
