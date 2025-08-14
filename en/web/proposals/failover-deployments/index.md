---
layout: default
title: Failover Deployments
permalink: /en/web/proposals/failover-deployments/
nav: false
---

{% include lang-toggle.html %}

# Failover Deployments

Weighted ALB target-group routing to enable zero-downtime **prod1 ↔ prod2** cutovers.

---

## Goal
- Send 100% traffic to **prod1** while deploying to **prod2**.
- Gradually shift traffic back to **prod2** (e.g., 90/10 → 75/25 → 50/50 → 25/75 → 0/100).
- Flip roles on the next deployment cycle (prod2 live, deploy to prod1).
- Return to even split after validation.
- Achieve this by converting Listener forwarding actions to **Weighted Target Groups** in the ALB.

---

<details markdown="1">
  <summary>Step-by-step plan (AWS Console)</summary>

### 1) Inspect current Listener rules
- AWS Console → **EC2 → Load Balancers**
- Select the **ALB** → **Listeners** tab → click **:443**
- Review rules that match host/path → forward to `-web-tg` or `-portal-tg`.

---

### 2) Convert fixed rule → Weighted Target Groups
**Goal:** Forward to both prod1 & prod2 target groups with adjustable weights.

**Example target groups:**
- `hankooktire-us-prd-<web|portal>-01-tg` (prod1)
- `hankooktire-us-prd-<web|portal>-02-tg` (prod2)

**How:**
1. Edit the rule.
2. Choose **Forward to → Weighted target groups**.
3. Add both TGs with initial weights:
   - `…-01-tg` → **100**
   - `…-02-tg` → **0**
4. Save.

---

### 3) Validate 100% on prod1
- All HTTPS traffic should hit **prod1**.
- **prod2** is idle and safe to deploy.
- Deploy to prod2 (`…-02-tg` instances).

---

### 4) Gradual traffic shift to prod2
1. Return to the Listener rule.
2. Adjust weights through stages, testing at each step:
   - 90/10 → 75/25 → 50/50 → 25/75 → 0/100 (or your chosen cadence).
3. Validate app behavior each step.
4. Monitor **CloudWatch** metrics (TG health, latency, 4xx/5xx).

---

### 5) Flip for next deployment
1. Set **prod1 TG** weight to **0**.
2. Deploy.
3. Ramp back to **100**.
4. Monitor, test, and finalize.

</details>

---

<details markdown="1">
  <summary>Things to note</summary>

- No additional AWS services or cost changes.
- Zero-downtime approach: weight **0** stops **new** connections but lets existing ones complete.
- TG stickiness is **off**, so sessions won’t cling to the old TG during ramp.
- Our broader deployment process remains unchanged.
- Coordinate with the team when performing a failover deployment.
- **Dev ALB** currently doesn’t mirror this setup:
  - Best practice: replicate weighted rules in **dev** and trial there first.

</details>

---

<details markdown="1">
  <summary>Expand: Debug / Render checks</summary>

Temporary collapsible to monitor styling and markdown processing.

```bash
echo "Hello from /en/web/proposals/failover-deployments/index.md within collapsible"
ls -la
```
</details>

### Render Sanity Check (outside collapsible)

```bash
echo "Hello from /en/web/proposals/failover-deployments/index.md outside collapsible"
```
