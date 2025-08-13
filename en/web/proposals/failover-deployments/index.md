---
layout: default
title: "📑 Failover Deployments"
lang: en
permalink: /en/web/proposals/failover-deployments/
---

{% include lang-toggle.html %}

# 📑 Failover Deployments

Weighted ALB target group routing to enable zero-downtime **prod1 ↔ prod2** cutovers.

---

## 🎯 Goal

- Send 100% traffic to **prod1** while deploying to **prod2**.
- Gradually shift traffic back to **prod2** (e.g., 10% → 25% → 50% → 100%).
- Flip roles on the next deployment cycle (prod2 live, deploy to prod1).
- Return to even split after validation.
- Implement by converting Listener forwarding actions to **Weighted Target Groups** in the ALB.

---

<!-- Pure-HTML collapsible to avoid Markdown parser issues -->
<details>
  <summary>🛠 STEP-BY-STEP PLAN (AWS Console)</summary>

  <h3>1) Inspect Current Listener Rules</h3>
  <ul>
    <li>AWS Console → <strong>EC2 → Load Balancers</strong></li>
    <li>Select the <strong>ALB</strong> → <strong>Listeners</strong> tab → click <strong>:443</strong></li>
    <li>Review rules that match host/path → forward to <code>-web-tg</code> or <code>-portal-tg</code>.</li>
  </ul>

  <hr />

  <h3>2) Convert Fixed Rule → Weighted Target Groups</h3>
  <p><strong>Goal:</strong> Forward to both prod1 &amp; prod2 target groups with adjustable weights.</p>

  <p><strong>Example target groups:</strong></p>
  <ul>
    <li><code>hankooktire-us-prd-&lt;web|portal&gt;-01-tg</code> (prod1)</li>
    <li><code>hankooktire-us-prd-&lt;web|portal&gt;-02-tg</code> (prod2)</li>
  </ul>

  <p><strong>How:</strong></p>
  <ol>
    <li>Edit the rule.</li>
    <li>Choose <strong>Forward to → Weighted target groups</strong>.</li>
    <li>Add both TGs with initial weights:
      <ul>
        <li><code>...-01-tg</code> → <strong>100</strong></li>
        <li><code>...-02-tg</code> → <strong>0</strong></li>
      </ul>
    </li>
    <li>Save.</li>
  </ol>

  <hr />

  <h3>3) Validate 100% on prod1</h3>
  <ul>
    <li>All HTTPS traffic should hit <strong>prod1</strong>.</li>
    <li><strong>prod2</strong> is idle and safe to deploy.</li>
    <li>Deploy to prod2 (<code>...-02-tg</code> instances).</li>
  </ul>

  <hr />

  <h3>4) Gradual Traffic Shift to prod2</h3>
  <ol>
    <li>Return to the Listener rule.</li>
    <li>Adjust weights through stages, testing at each step:
      <ul>
        <li>90/10 → 75/25 → 50/50 → 25/75 → 0/100 (or your chosen cadence).</li>
      </ul>
    </li>
    <li>Validate app behavior each step.</li>
    <li>Monitor <strong>CloudWatch</strong> metrics (TG health, latency, 4xx/5xx).</li>
  </ol>

  <hr />

  <h3>5) Flip for Next Deployment</h3>
  <ol>
    <li>Set <strong>prod1 TG</strong> weight to <strong>0</strong>.</li>
    <li>Deploy.</li>
    <li>Ramp back to <strong>100</strong>.</li>
    <li>Monitor, test, and finalize.</li>
  </ol>

</details>

---

<details>
  <summary>📌 Things to Note</summary>

  <ul>
    <li>No additional AWS services or cost changes.</li>
    <li>Zero-downtime approach: weight <code>0</code> stops <strong>new</strong> connections but lets existing ones complete.</li>
    <li>TG stickiness is <strong>off</strong>, so sessions won’t cling to the old TG during ramp.</li>
    <li>Our broader deployment process remains unchanged.</li>
    <li>Coordinate with the team when performing a failover deployment.</li>
    <li><strong>Dev ALB</strong> currently doesn’t mirror this setup:
      <ul>
        <li>Best practice: replicate weighted rules in <strong>dev</strong> and trial there first.</li>
      </ul>
    </li>
  </ul>

</details>
