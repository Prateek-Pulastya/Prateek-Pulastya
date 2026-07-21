<h1>Prateek Pulastya</h1>

<p><strong>Security Engineer — AI Security &amp; Application Security</strong><br>
Berlin, Germany · Open to security engineering roles (EU)</p>

<p>
<a href="https://prateek-pulastya.github.io/"><img alt="Portfolio" src="https://img.shields.io/badge/Portfolio-0F172A?style=flat-square&logo=githubpages&logoColor=white"></a>
<a href="https://www.linkedin.com/in/prateek-pulastya22/"><img alt="LinkedIn" src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white"></a>
<a href="https://medium.com/@prateekpulastya"><img alt="Medium" src="https://img.shields.io/badge/Write--ups-12100E?style=flat-square&logo=medium&logoColor=white"></a>
<a href="mailto:prateekpulastya220@gmail.com"><img alt="Email" src="https://img.shields.io/badge/Email-334155?style=flat-square&logo=gmail&logoColor=white"></a>
</p>

I build and break the security layer around LLM applications. Most of my time goes to
prompt-injection defence, API and application security testing, and turning findings into
tooling that survives contact with production traffic.

Currently an independent security researcher (private bug bounty and coordinated
disclosure), finishing an **MSc in Artificial Intelligence** in Berlin, after an
**MSc in Cyber Security** and four years across penetration testing and security
engineering.

---

## GuardRail-as-a-Service

Two-tier prompt-injection detection for production LLM serving. Sub-millisecond on the
common path, evaluated against four external benchmarks.

**[→ Guardrail-As-A-Service-V2](https://github.com/Prateek-Pulastya/Guardrail-As-A-Service-V2)** · Python · Docker · ONNX · Prometheus

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

## Vulnerability research

Private bug bounty and coordinated disclosure. Statuses are reported as they resolved —
duplicates and informatives included.

| Finding | Class | Impact | Status |
|---|---|---|---|
| Python sandbox escape in `smolagents` | CWE-94 · **CVSS 9.9** | Arbitrary host command execution | Disclosed via huntr |
| Path-traversal detection bypass, Aikido `firewall-java` | Security-control bypass | Defeats WAF path-traversal detection | Disclosed via Intigriti |
| Unauthenticated GraphQL bulk pagination | API1 / API4 | **57.3M** user records enumerable, no rate limit | Duplicate (confirmed valid) |
| Unrestricted Google Maps API keys in page source | CWE-798 | ~$121/hr billable abuse, measured | Duplicate / P4 |
| CORS origin reflection + `credentials: true` | CWE-942 | Full account takeover via one link | Duplicate |
| Dangling Route53 NS delegation | Subdomain takeover | HTTPS phishing + session-cookie theft | Informative |

**🥇 #1 Quarterly Leaderboard** (RO07 Ch13f) and **Top 10 Quarterly** (Bug Baron) on Intigriti.

Tooling: Burp Suite Pro · Semgrep · libFuzzer / CI Fuzz · custom Python recon and
validation harnesses.

---

## Other work

| Project | What it does |
|---|---|
| [AI-Powered Threat Detection](https://github.com/Prateek-Pulastya/AI-Powered-Threat-Detection-System-with-Explainability) | Network IDS on CICIDS2017 across 6 attack classes, with SHAP explanations so analysts get *why*, not just a label |
| [Hydroficient IoT Externship](https://github.com/Prateek-Pulastya/Hydroficient-Externship) | STRIDE-modelled MQTT pipeline hardened with TLS 1.3/mTLS, HMAC-SHA256, replay defence — validated by live attack simulation per layer. *Top Performer, top 10%* |
| [Outamation Externship](https://github.com/Prateek-Pulastya/Outamation-Externship) | Document-intelligence pipeline over 200+ page mortgage blobs — OCR, LlamaIndex RAG, open-source LLM evaluation |

---

## Toolchain

**AI / LLM security** — prompt injection · RAG security · OWASP LLM Top 10 · NIST AI RMF · garak · ONNX Runtime · PyTorch · Transformers · SHAP

**Offensive** — Burp Suite Pro · Nmap · Nessus · Semgrep · libFuzzer / CI Fuzz · threat modelling (STRIDE)

**Detection & response** — Microsoft Sentinel · Defender for Endpoint · Splunk · Prometheus · Grafana

**Cloud & platform** — AWS · Azure · OCI · Terraform · Docker · GitHub Actions

**Languages** — Python · Bash · PowerShell · SQL

---

## Certifications

| Credential | Issuer | Date |
|---|---|---|
| Certified LLM Security Professional (CLLMSP) | Red Team Leaders | Jun 2026 |
| Fortinet Certified Associate in Cybersecurity | Fortinet | Oct 2025 → Oct 2027 |
| OCI 2025 Certified AI Foundations Associate | Oracle | Aug 2025 |
| Certified Network Security Specialist (CNSS) | ICSI, UK | Jul 2020 |

---

## Writing

Long-form technical write-ups on [Medium](https://medium.com/@prateekpulastya) — bug bounty
methodology, CTF chains, and the reasoning behind findings, including the ones that came
back as duplicates.

---

<sub>English (professional) · German (A2, improving) · Spanish (elementary)</sub>
