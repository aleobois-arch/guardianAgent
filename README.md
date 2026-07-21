# 🛡️ GuardianAgent

<p align="center"><b>GuardianAgent — AI Security Gate & Compliance Orchestrator</b></p>

**GuardianAgent** is the **GPT-native evolution** of [`guardagent-control-plane`](https://github.com/wecanmoove/guardagent-control-plane) — rebuilt from the ground up for **GPT-5.6** and developed interactively with **OpenAI Codex**. Where the original control-plane used Gemini 2.5 Flash on Google Cloud, GuardianAgent is entirely OpenAI-native: GPT-5.6 drives the risk reasoning engine, and every line of core functionality was either scaffolded or refined inside a Codex session.

> ⚠️ Built for the **OpenAI Codex hackathon** (July 2026). Demo data is simulated; the GPT-5.6 reasoning core, NIST CSF 2.0 engine, agent policy enforcement, and audit persistence are real.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Python 3.12+](https://img.shields.io/badge/python-3.12%2B-blue.svg)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.111-009688.svg)](https://fastapi.tiangolo.com)
[![Powered by GPT-5.6](https://img.shields.io/badge/GPT--5.6-Powered-412991.svg)](https://openai.com)
[![Built with Codex](https://img.shields.io/badge/Built%20with-OpenAI%20Codex-000000.svg)](https://openai.com/codex)

---

## Origin — guardagent-control-plane vs. GuardianAgent

| | [`guardagent-control-plane`](https://github.com/wecanmoove/guardagent-control-plane) | **GuardianAgent (this repo)** |
|---|---|---|
| AI reasoning core | Gemini 2.5 Flash (Google Vertex AI) | **GPT-5.6 (OpenAI)** |
| Built with | Manual coding + Gemini prompting | **OpenAI Codex — interactive sessions** |
| Cloud target | Google Cloud Run + Vertex AI | OCI, Azure, Alibaba Cloud, GitHub Actions |
| Compliance framework | NIST CSF 2.0 (partial) | **NIST CSF 2.0 — fully mapped, weighted** |
| Secret detection | 18-rule deterministic engine | **200+ patterns + entropy scoring** |
| Agent guardrails | Policy engine (`agent_policy.py`) | **GPT-5.6 behavioral anomaly detection** |
| Executive narrative | Gemini-generated | **GPT-5.6 — CISO-grade prose** |
| CI/CD gate | Cloud Build only | **GitHub Actions, OCI DevOps, Azure Pipelines** |
| Frontend | Single-file HTML dashboard | Single-file HTML dashboard (same pattern) |

---

## How I Collaborated with Codex

### The Collaboration Story

This entire project was built in partnership with **OpenAI Codex** across focused, iterative sessions. Here is exactly how that collaboration shaped each layer of the product.

#### 🧠 Phase 1 — Architecture (Codex as Thought Partner)

I described the evolution goal to Codex:

> *"I have guardagent-control-plane using Gemini on GCP. I want to port the reasoning core to GPT-5.6, extend the secret detection to 200+ patterns with entropy scoring, and make the CI/CD gate work natively on GitHub Actions, OCI DevOps, and Azure Pipelines. Keep the single-file dashboard pattern."*

Codex generated the initial multi-agent topology — Scanner Agent → Risk Evaluator (GPT-5.6) → Gate Enforcer → Reporter — in minutes. What would have been a day of architecture sketching became a 30-minute conversation with immediate scaffolding.

#### ⚡ Phase 2 — Core Development (Where Codex Accelerated the Most)

1. **Secret pattern engine** — I gave Codex the taxonomy (AWS keys, OpenAI tokens, OCI credentials, Databricks tokens, Snowflake passwords, Stripe keys, GitHub PATs, generic API keys). Codex wrote all 200+ regex patterns, entropy filters, and the full test suite in a single session. Estimated time saved: **6–8 hours**.

2. **NIST CSF 2.0 mapper** — I provided the framework subcategory list (GV, ID, PR, DE, RS, RC functions). Codex generated the complete control-to-finding mapping and the weighted scoring algorithm. I then calibrated the weights based on my experience delivering compliance for enterprise clients (Oracle EBS, Azure, Databricks environments).

3. **FastAPI route layer** — I described the 14 endpoints I needed in natural language. Codex generated all routes, Pydantic models, auth middleware, and error handlers. I focused on the business logic and security model rather than boilerplate.

4. **GitHub Actions YAML** — From a single prompt describing the desired pipeline behaviour, Codex generated the full matrix build, caching strategy, conditional gate logic, and artifact upload steps.

5. **docker-compose demo stack** — Codex assembled the multi-service compose file (API + static dashboard via nginx) from a plain description of the local demo requirements.

#### 🎯 Phase 3 — Key Decisions Were Mine

Codex accelerates; it does not decide. Every product and architecture decision that shapes GuardianAgent's identity came from me:

- **Choosing GPT-5.6 over GPT-4o** for the risk reasoning core — GPT-5.6's superior multi-step reasoning significantly improves the quality of NIST control mappings and executive narratives, which I verified by comparing outputs side-by-side.
- **Capping the Gate Enforcer at "recommend-then-confirm"** — after testing showed false positives in monorepo environments, I deliberately chose not to hard-block by default. The `gate_mode: advisory | warn | hard` ladder was my design.
- **The "Explain & Remediate" requirement** — the original control-plane flagged issues. GuardianAgent requires every finding to carry a plain-language explanation, a severity score, a remediation recipe, and an estimated effort in hours. This came from practitioner feedback on the v1.
- **Multi-cloud first** — OCI, Azure, and Alibaba Cloud are supported from day one because ALEODATA's client base spans all three. This is a product decision rooted in real delivery experience, not a Codex suggestion.
- **Privacy-preserving findings store** — secrets detected during scanning are stored as hashed references only, never plaintext. I specified this constraint explicitly; Codex implemented it.

#### 🔁 Phase 4 — Iterative Refinement with GPT-5.6

Once the Codex sessions produced the working skeleton, I used **GPT-5.6 in chat mode** for:
- Edge-case analysis on the risk scoring algorithm (particularly for monorepo polyglot repos)
- Validating NIST CSF 2.0 subcategory assignments for ambiguous findings
- Generating adversarial test scenarios for the AI agent guardrails module (prompt injection, jailbreak simulation)
- Drafting the executive risk narratives that the Reporter Agent surfaces to CISOs

GPT-5.6's extended reasoning caught subtle errors in control weighting that code generation alone would never have surfaced.

---

## Where GPT-5.6 & Codex Contributed

| Component | GPT-5.6 Role | Codex Role | My Role |
|---|---|---|---|
| Secret pattern engine (200+ rules) | Reviewed entropy logic | Wrote all regex + full test suite | Defined secret taxonomy |
| NIST CSF 2.0 mapper | Validated control mappings | Generated scaffold + scoring fn | Framework selection, weight calibration |
| Agent orchestration layer | Reviewed agent design | Scaffolded all agent classes | Architecture & autonomy decisions |
| Risk scoring algorithm | Edge-case analysis | Initial scoring function | Calibration, tuning, false-positive policy |
| FastAPI REST API (14 routes) | — | Generated all routes + models | Business logic, auth model, rate limiting |
| GitHub Actions integration | — | Generated full YAML | Pipeline design, gate-mode ladder |
| Executive risk narrative | Drafted CISO narrative templates | Generated report structure | Tailored for non-technical executives |
| Frontend dashboard | — | Generated chart + module components | UX decisions, module selection |
| Unit + integration test suite | Generated adversarial scenarios | Wrote all test code | Test strategy, coverage targets |
| docker-compose demo stack | — | Generated compose file | Service topology, port mapping |

### GPT-5.6's Specific Contributions

GPT-5.6 was indispensable for **compliance reasoning** tasks that require understanding regulatory *intent*, not just pattern matching:

1. **Ambiguous NIST CSF 2.0 mappings** — when a finding could map to multiple subcategories, GPT-5.6 provided nuanced guidance on the most defensible primary mapping, citing framework rationale.
2. **CISO-grade narrative generation** — GPT-5.6 produces executive summaries that are technically accurate and readable by non-technical board-level stakeholders simultaneously. This balance was not achievable with prior models.
3. **Adversarial guardrail testing** — I used GPT-5.6 to generate prompt-injection and jailbreak attempts against the AI agent guardrails module, stress-testing the detection logic before shipping.

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        GuardianAgent                            │
│                                                                 │
│  ┌──────────────┐   ┌──────────────┐   ┌──────────────────┐   │
│  │ Scanner      │   │ Risk         │   │ Gate Enforcer    │   │
│  │ Agent        │──▶│ Evaluator    │──▶│ Agent            │   │
│  │              │   │ (GPT-5.6)    │   │                  │   │
│  │ • 200+ rules │   │ • NIST CSF   │   │ • GitHub Actions │   │
│  │ • Entropy    │   │ • Scoring    │   │ • OCI DevOps     │   │
│  │ • IaC audit  │   │ • Narrative  │   │ • Azure Pipelines│   │
│  └──────────────┘   └──────────────┘   └──────────────────┘   │
│                              │                                  │
│                     ┌────────▼────────┐                        │
│                     │ Reporter Agent  │                        │
│                     │ • Risk Dashboard│                        │
│                     │ • CISO Reports  │                        │
│                     │ • Slack / Teams │                        │
│                     └─────────────────┘                        │
└─────────────────────────────────────────────────────────────────┘
```

---

## Features

- 🔑 **200+ secret patterns** — API keys, tokens, credentials, certificates, private keys
- 📋 **NIST CSF 2.0 full mapping** — every finding auto-mapped to framework subcategories with weighted scoring
- 🤖 **AI agent guardrails** — GPT-5.6 detects prompt injection and behavioural anomalies in downstream agents
- ⚡ **Sub-second scanning** — async parallel processing for large repositories
- 🚦 **Pipeline gates** — `advisory | warn | hard` modes for GitHub Actions, OCI DevOps, Azure Pipelines
- 📊 **Risk trend dashboard** — single-file HTML (same pattern as `guardagent-control-plane`)
- 📧 **Multi-channel alerts** — Slack, Teams, PagerDuty, email
- 🌍 **Multi-cloud policies** — OCI, Azure, Alibaba Cloud, AWS
- 🔒 **Privacy-preserving** — secrets never logged in plaintext (hashed references only)
- 📄 **GPT-5.6 executive reports** — CISO-ready narratives generated by the model

---

## Installation

### Prerequisites

- Python 3.12+
- OpenAI API key with access to GPT-5.6 (or GPT-4o as fallback)
- Git 2.30+

### Option 1 — pip install (Recommended)

```bash
pip install guardianagent
```

### Option 2 — From Source

```bash
git clone https://github.com/aleobois-arch/guardianAgent.git
cd guardianAgent
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
export OPENAI_API_KEY="sk-..."
```

### Option 3 — Docker

```bash
docker run -e OPENAI_API_KEY=sk-... \
  -v $(pwd):/repo \
  wecanmoove/guardian-agent:latest scan /repo
```

### GitHub Actions Integration

Add to `.github/workflows/security.yml`:

```yaml
name: GuardianAgent Security Gate

on: [push, pull_request]

jobs:
  guardian:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0  # Full history for commit scanning

      - name: Run GuardianAgent
        uses: aleobois-arch/guardianAgent@v1
        with:
          openai-api-key: ${{ secrets.OPENAI_API_KEY }}
          nist-profile: 'enterprise'       # starter | enterprise | critical
          gate-mode: 'hard'                # advisory | warn | hard
          notify-slack: ${{ secrets.SLACK_WEBHOOK }}
```

---

## Supported Platforms

| Platform | Integration | Status |
|---|---|---|
| GitHub Actions | Native action (`uses:`) | ✅ GA |
| GitLab CI | REST API + pipeline script | ✅ GA |
| OCI DevOps | REST API + build spec | ✅ GA |
| Azure Pipelines | REST API + pipeline task | ✅ GA |
| Alibaba Cloud DevOps | REST API | ✅ GA |
| Bitbucket Pipelines | REST API | 🔶 Beta |
| Jenkins | Plugin (Groovy DSL) | 🔶 Beta |
| CLI (local) | `guardian scan .` | ✅ GA |

**OS Support:** Linux, macOS, Windows (WSL2 recommended)  
**Python:** 3.11, 3.12, 3.13

---

## Quick Start — Test Without Rebuilding

### 🌐 Live Demo Dashboard

The static dashboard (same single-file pattern as `guardagent-control-plane`) is available at:

**➡️ [https://wecanmoove.github.io/guardagent-control-plane/](https://wecanmoove.github.io/guardagent-control-plane/)**

This gives judges an immediate feel for the UI/UX and dashboard modules without any setup.

### 🧪 API Sandbox

Test the scanning API directly:

```bash
curl -X POST https://guardian-api.aleodata.com/v1/scan \
  -H "Authorization: Bearer DEMO-TOKEN-2026" \
  -H "Content-Type: application/json" \
  -d '{
    "repo_url": "https://github.com/wecanmoove/guardagent-control-plane",
    "scan_mode": "full",
    "nist_profile": "starter"
  }'
```

Demo credentials:
- **API Token:** `DEMO-TOKEN-2026`
- **Dashboard login:** `judge@demo.com` / `guardian2026`

### 🐳 One-Command Docker Demo

```bash
docker compose -f docker-compose.demo.yml up
# Dashboard: http://localhost:3000
# API docs:  http://localhost:8000/docs
```

### 💻 CLI Quick Test

```bash
pip install guardianagent
export OPENAI_API_KEY="your-key"
guardian scan --repo https://github.com/wecanmoove/guardagent-control-plane --demo
```

---

## API

| Endpoint | What it does |
|---|---|
| `POST /v1/scan` | Scan a repo — deterministic engine + GPT-5.6 reasoning → NIST verdict + gate decision |
| `POST /v1/agent/guard` | Evaluate an AI-agent action against the execution policy **before** it runs |
| `GET /v1/scan/{id}/findings` | Retrieve full findings with NIST mappings + remediation recipes |
| `GET /v1/scan/{id}/narrative` | GPT-5.6 executive narrative for a completed scan |
| `GET /v1/scans` · `/v1/stats` | Persisted scan history + trend data for dashboard |
| `GET /health` | Liveness + GPT-5.6 availability + counters |

---

## Dashboard Modules

Executive Risk Dashboard · Commit Risk Triage · AI Code Inspection (live GPT-5.6 verdicts) · Pipeline Gate Center · Agent Security Console · Threat & Exposure Watch · **NIST CSF 2.0 Governance Center** · Evidence & Audit Trail (JSON/CSV export).

---

## Codex Session Reference

> **Codex Session ID:** Submitted via `/feedback` in the project thread.
>
> The majority of core functionality — the 200+ secret pattern engine, NIST CSF 2.0 mapper, multi-agent orchestration scaffold, all 14 FastAPI routes, the GitHub Actions integration, and the test suite — was built in Codex sessions. The session thread documents the full iterative arc: initial architecture prompts, scaffolding outputs, my refinement decisions, and the specific moments where product judgment diverged from Codex's initial suggestions.

---

## Tech Stack

- **AI Core:** OpenAI GPT-5.6, OpenAI Codex
- **Backend:** Python 3.12, FastAPI, asyncio
- **Secret Detection:** Custom regex engine + Shannon entropy analysis
- **Compliance Framework:** NIST CSF 2.0
- **CI/CD Integration:** GitHub Actions, OCI DevOps, Azure Pipelines
- **Frontend:** Single-file HTML5 + vanilla JS (zero-framework — same pattern as `guardagent-control-plane`)
- **Infrastructure:** Docker, docker-compose, OCI Functions
- **Databases:** SQLite (dev), PostgreSQL (prod)
- **Notifications:** Slack Webhooks, Microsoft Teams Adaptive Cards

---

## Related Repositories

| Repo | Role |
|---|---|
| [`guardagent-control-plane`](https://github.com/wecanmoove/guardagent-control-plane) | Original — Gemini 2.5 Flash on Google Cloud |
| [`compliance-guardian-flask`](https://github.com/wecanmoove/compliance-guardian-flask) | Contract risk intelligence (Flask, v1.3.1) |
| [`compliance-guardian-api-python`](https://github.com/wecanmoove/compliance-guardian-api-python) | FastAPI backend, BCM/DRP scoring |
| [`Compliance-Guardian-Copilot`](https://github.com/wecanmoove/Compliance-Guardian-Copilot) | Azure AI + ML contract analysis (C#) |

---

## License

MIT — See [LICENSE](LICENSE)

---

*GuardianAgent — GPT-5.6 reasoning core · NIST CSF 2.0 governance · Built with OpenAI Codex*  
*[Christopher Messana](https://github.com/wecanmoove) @ [ALEODATA](https://aleodata.com) — Provence, France 🇫🇷*
