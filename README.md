<!-- ============================================================
     Recruiter-oriented layout, self-contained (shields.io + GitHub
     avatar only — no third-party widget services that can 503 or
     rate-limit the page). Content is honest and security-focused.
     ============================================================ -->

<div align="center">
<table width="100%">
<tr>
<td width="66%" valign="middle">

<sub>SECURITY ENGINEER · BERLIN, GERMANY · OPEN TO EU ROLES</sub>

<h1>Prateek Pulastya</h1>
<h3>Security Engineer — AI Security &amp; Application Security</h3>

<p>I build and break the security layer around LLM applications — prompt-injection
defence, API and application security testing, and turning findings into tooling
that survives contact with production traffic.</p>

<p><strong>● Independent security researcher · finishing an MSc in AI · #1 Intigriti quarterly leaderboard</strong></p>

<p>
<a href="https://prateek-pulastya.github.io/"><img alt="Portfolio" src="https://img.shields.io/badge/Portfolio-0F172A?style=flat-square&logo=githubpages&logoColor=white"></a>
<a href="https://www.linkedin.com/in/prateek-pulastya22/"><img alt="LinkedIn" src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white"></a>
<a href="https://medium.com/@prateekpulastya"><img alt="Write-ups" src="https://img.shields.io/badge/Write--ups-12100E?style=flat-square&logo=medium&logoColor=white"></a>
<a href="mailto:prateekpulastya220@gmail.com"><img alt="Email" src="https://img.shields.io/badge/Email-334155?style=flat-square&logo=gmail&logoColor=white"></a>
</p>

</td>
<td width="34%" valign="middle" align="center">
<img src="https://avatars.githubusercontent.com/u/78462354?v=4" width="190" alt="Prateek Pulastya">
</td>
</tr>
</table>
</div>

<h2>What a team can evaluate in 15 seconds</h2>

<table width="100%">
<tr>
<td width="33%" valign="top"><h3>Role fit</h3><p>Security Engineer — AI/LLM security, application &amp; product security, vulnerability research.</p></td>
<td width="33%" valign="top"><h3>Focus</h3><p>Prompt-injection defence · detection engineering · secure code review · coordinated disclosure.</p></td>
<td width="33%" valign="top"><h3>Availability</h3><p>Berlin, Germany · open to security roles across the EU. Dual MSc (Cyber Security + AI, in progress).</p></td>
</tr>
</table>

<h2>Proof at a glance</h2>

<table width="100%">
<tr>
<td width="25%" align="center"><strong>#1</strong><br /><sub>Intigriti quarterly<br />leaderboard (RO07&nbsp;Ch13f)</sub></td>
<td width="25%" align="center"><strong>CVSS&nbsp;9.9</strong><br /><sub>disclosed sandbox<br />escape (CWE-94)</sub></td>
<td width="25%" align="center"><strong>0.7895</strong><br /><sub>held-out recall —<br />the honest number</sub></td>
<td width="25%" align="center"><strong>4</strong><br /><sub>external benchmarks<br />on the flagship</sub></td>
</tr>
</table>

---

## GuardRail-as-a-Service — the flagship

Two-tier prompt-injection detection for production LLM serving. Sub-millisecond on the
common path, evaluated against four external benchmarks.

**[→ Guardrail-As-A-Service-V2](https://github.com/Prateek-Pulastya/Guardrail-As-A-Service-V2)**

<p>
<img src="https://img.shields.io/badge/Python-3670A0?style=flat-square&logo=python&logoColor=white">
<img src="https://img.shields.io/badge/ONNX-005CED?style=flat-square&logo=onnx&logoColor=white">
<img src="https://img.shields.io/badge/DeBERTa--v3-EE4C2C?style=flat-square&logo=pytorch&logoColor=white">
<img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white">
<img src="https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white">
<img src="https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white">
</p>

| Evaluation | Tier 1 recall | FPR |
|---|---|---|
| In-house corpus (in-sample) | 1.000 | 0.000 |
| **Held-out split — the honest number** | **0.7895** | 0.000 |
| Open-Prompt-Injection (`source="data"`) | 1.000 | 0.006 |
| BIPIA (`source="data"`) | 0.480 | 0.017 |
| NotInject (over-defense, benign only) | — | 0.000 |

> The headline result is not the 1.000. It is the **21-point gap** between the in-sample
> score and the held-out one. Tier 1's blocklist was tuned by inspecting the attacks it
> missed *on that corpus*, so the perfect score is partly memorisation — the repo says so,
> quantifies it, and ships the split script that proves it.

Design decisions I can defend in an interview:

- **Tier 1** — Aho-Corasick + regex over normalised text, scanned twice: once preserving
  structural markers (`<|im_start|>`, `safety_mode=off`), once de-obfuscated to catch
  `1gn0r3 prev10us 1nstruct10ns`. p50 **0.14 ms**.
- **Tier 2 is monitor-only, deliberately.** DeBERTa-v3 ONNX scores and logs but does not
  block, because on NotInject it rejects **40.4% of benign prompts** against Tier 1's 0.0%,
  and the over-defense is not threshold-separable. The cost is a recall ceiling. Both
  operating points are published.
- **Fail-open.** If the Tier 2 model errors, the request is allowed. Availability over
  semantic coverage, stated rather than defaulted into.
- A content-safety baseline (Llama-Guard-3-8B) misses 165/190 attacks here — reported as
  *"content-safety guardrails don't transfer to prompt injection"*, **not** as a 7× win.

---

## Selected work

<table width="100%">
<tr>
<td width="50%" valign="top">
<h3><a href="https://github.com/Prateek-Pulastya/cloudfracture">cloudfracture</a></h3>
<p>Deliberately vulnerable AWS AI-agent security lab — attack, detect, remediate. Terraform-provisioned, with Sigma detections and an AppSec CI gate.</p>
<p><sub>Python · Terraform · Sigma · AWS</sub></p>
</td>
<td width="50%" valign="top">
<h3><a href="https://github.com/Prateek-Pulastya/soc-detection-lab">soc-detection-lab</a></h3>
<p>Home SOC detection-engineering lab: Wazuh + Sysmon, ATT&amp;CK techniques detonated with Atomic Red Team, caught with hand-authored Sigma rules, plus an evaluated AI triage layer — <strong>7/10 detected, gaps documented</strong>.</p>
<p><sub>Wazuh · Sysmon · MITRE ATT&amp;CK · Sigma</sub></p>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<h3><a href="https://github.com/Prateek-Pulastya/securefix">securefix</a></h3>
<p>Six web vulnerabilities (SQLi, IDOR, SSRF, XSS, JWT-bypass, prototype pollution), each with a working exploit, a fix, a custom Semgrep rule, and a CI gate that fails the build if it returns. SAST gate goes 7 → 0.</p>
<p><sub>TypeScript · Semgrep · CI/CD · OWASP</sub></p>
</td>
<td width="50%" valign="top">
<h3><a href="https://github.com/Prateek-Pulastya/ATSGuard">ATSGuard</a></h3>
<p>Stops indirect prompt injection — hidden white-on-white instructions in a résumé that hijack an LLM applicant tracking system. 0% false positives across 1,200 résumés; 98.8% in-sample recall, 42.9% held-out (reported honestly).</p>
<p><sub>Python · OWASP LLM01 · Unicode normalisation</sub></p>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<h3><a href="https://github.com/Prateek-Pulastya/AI-Powered-Threat-Detection-System-with-Explainability">AI-Powered Threat Detection</a></h3>
<p>Network IDS on CICIDS2017 across six attack classes with SHAP explanations, so an analyst gets <em>why</em> a flow was flagged, not just a label.</p>
<p><sub>Python · scikit-learn · SHAP · CICIDS2017</sub></p>
</td>
<td width="50%" valign="top">
<h3><a href="https://github.com/Prateek-Pulastya/security-compliance-academy">security-compliance-academy</a></h3>
<p>Cited, machine-readable control-to-framework crosswalk — ISO 27001, NIST CSF, SOC 2, CIS, GDPR — with a confidence grade and primary-source URL per mapping, published as a fetchable dataset and validated in CI.</p>
<p><sub>Next.js · GRC · ISO 27001 · SOC 2</sub></p>
</td>
</tr>
</table>

---

## Vulnerability research

Private bug bounty and coordinated disclosure. Statuses are reported as they resolved —
duplicates and informatives included, because the methodology is the transferable part.

| Finding | Class | Impact | Status |
|---|---|---|---|
| Python sandbox escape in `smolagents` | CWE-94 · **CVSS 9.9** | Arbitrary host command execution | Disclosed via huntr |
| Path-traversal detection bypass, Aikido `firewall-java` | Security-control bypass | Defeats WAF path-traversal detection | Disclosed via Intigriti |
| Unauthenticated GraphQL bulk pagination | API1 / API4 | **57.3M** user records enumerable, no rate limit | Duplicate (confirmed valid) |
| Unrestricted Google Maps API keys in page source | CWE-798 | ~$121/hr billable abuse, measured | Duplicate / P4 |
| CORS origin reflection + `credentials: true` | CWE-942 | Full account takeover via one link | Duplicate |
| Dangling Route53 NS delegation | Subdomain takeover | HTTPS phishing + session-cookie theft | Informative |

**🥇 #1 Quarterly Leaderboard** (RO07 Ch13f) and **Top 10 Quarterly** (Bug Baron) on Intigriti.

---

## Toolchain

<p>
<img src="https://img.shields.io/badge/Python-3670A0?style=flat-square&logo=python&logoColor=white">
<img src="https://img.shields.io/badge/Bash-4EAA25?style=flat-square&logo=gnubash&logoColor=white">
<img src="https://img.shields.io/badge/PowerShell-5391FE?style=flat-square&logo=powershell&logoColor=white">
<img src="https://img.shields.io/badge/SQL-336791?style=flat-square&logo=postgresql&logoColor=white">
<img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white">
</p>
<p>
<img src="https://img.shields.io/badge/Burp_Suite_Pro-FF6633?style=flat-square&logo=burpsuite&logoColor=white">
<img src="https://img.shields.io/badge/Semgrep-1B2A4A?style=flat-square&logo=semgrep&logoColor=white">
<img src="https://img.shields.io/badge/Nmap-4682B4?style=flat-square&logo=nmap&logoColor=white">
<img src="https://img.shields.io/badge/Wireshark-1679A7?style=flat-square&logo=wireshark&logoColor=white">
<img src="https://img.shields.io/badge/MITRE_ATT%26CK-C1272D?style=flat-square&logo=mitre&logoColor=white">
<img src="https://img.shields.io/badge/Sigma_rules-EF3B2D?style=flat-square">
</p>
<p>
<img src="https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonwebservices&logoColor=white">
<img src="https://img.shields.io/badge/Azure-0078D4?style=flat-square&logo=microsoftazure&logoColor=white">
<img src="https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white">
<img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white">
<img src="https://img.shields.io/badge/Microsoft_Sentinel-0078D4?style=flat-square&logo=microsoft&logoColor=white">
<img src="https://img.shields.io/badge/Splunk-000000?style=flat-square&logo=splunk&logoColor=white">
</p>
<p>
<img src="https://img.shields.io/badge/ONNX_Runtime-005CED?style=flat-square&logo=onnx&logoColor=white">
<img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white">
<img src="https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white">
<img src="https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white">
<img src="https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white">
</p>

**Domains** — AI/LLM security (prompt injection · RAG security · OWASP LLM Top 10 · NIST AI RMF · guardrail architecture) · application &amp; API security (OWASP Top 10 · STRIDE threat modelling · secure code review · detection-as-code) · offensive security &amp; vulnerability research · detection engineering · cloud &amp; GRC (ISO 27001 · NIST CSF · SOC 2 · GDPR).

---

## Certifications

| Credential | Issuer | Date |
|---|---|---|
| AWS Certified Security — Specialty | Amazon Web Services | Aug 2026 → Aug 2029 |
| AWS Certified Solutions Architect — Associate | Amazon Web Services | Aug 2026 → Aug 2029 |
| Certified LLM Security Professional (CLLMSP) | Red Team Leaders | Jun 2026 |
| Fortinet Certified Associate in Cybersecurity | Fortinet | Oct 2025 → Oct 2027 |
| OCI 2025 Certified AI Foundations Associate | Oracle | Aug 2025 |
| Certified Network Security Specialist (CNSS) | ICSI, UK | Jul 2020 |

---

<div align="center">
<table width="100%">
<tr>
<td width="62%" valign="middle">
<h2>Let's talk security</h2>
<p>Open to AI/LLM security, application &amp; product security, and detection-engineering roles across the EU. Happy to walk through any result here — including the ones that came back as duplicates.</p>
</td>
<td width="38%" valign="middle" align="right">
<a href="https://prateek-pulastya.github.io/">Portfolio</a><br />
<a href="https://www.linkedin.com/in/prateek-pulastya22/">LinkedIn</a><br />
<a href="https://medium.com/@prateekpulastya">Medium write-ups</a><br />
<a href="mailto:prateekpulastya220@gmail.com">prateekpulastya220@gmail.com</a>
</td>
</tr>
</table>
</div>

<sub>English (professional) · German (A2, improving) · Spanish (elementary)</sub>
