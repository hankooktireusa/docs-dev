---
layout: default
title: Deployment
permalink: /en/web/deployment-automation/
nav: true
---

{% include lang-toggle.html %}

# Deployment Automation

This project automates deployments for **CustomerPortal (CP)** and **WebOrder (WO)** to DEV and PROD using PowerShell, WinSCP, and PuTTY.

---

## Download Scripts

1. [Download the ZIP]({{ '/assets/downloads/deployment-automation-scripts.zip' | relative_url }})
2. Extract to:
   ```text
   C:\scripts\deployment-automation
   ```
3. Open PowerShell and run:
   ```powershell
   .\main.ps1
   ```

For full setup and configuration details, see the **README.md inside the ZIP**.

---

## Features
- Environment-aware config switching (datasource, SAP, WSDL)
- Optional Maven build step
- Safe WAR/ROOT backup and transfer via WinSCP
- Dynamic SSH host key trust for PuTTY and WinSCP
- PuTTY automation for Tomcat restart and live log monitoring
- Seamless PROD1 → PROD2 continuation using the same WAR file
- Post-deployment prompts, rollback, and cleanup support

---

## Script Structure (included in ZIP)
```yaml
deployment-automation/
├── config.ps1                           # Shared paths, session names, and SSH host keys
├── main.ps1                             # Main entry point to automate full deployment
├── README.md                            # Full usage guide and setup instructions
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

## Deployment Flow Overview
```
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
```

---

## New Developers
This tool walks you through the full deployment flow for CP and WO with prompts, verifications, and safe rollback. Ask a teammate to shadow your first run.

---

<details markdown="1">
  <summary>Expand: Debug / Render checks</summary>

Temporary collapsible to monitor styling and markdown processing.

```bash
echo "Hello from /en/web/deployment-automation/index.md within collapsible"
ls -la
```
</details>

### Render Sanity Check (outside collapsible)

```bash
echo "Hello from /en/web/deployment-automation/index.md outside collapsible"
```
