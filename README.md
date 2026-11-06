<div align="center">

# OpsMemory AI 🧠⚡

**Persistent-Memory Incident Response Platform for Software Operations**

[![Status: Verified](https://img.shields.io/badge/Status-VERIFIED-10B981.svg?style=flat-square)](IMPLEMENTATION_STATUS.md)
[![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-06B6D4.svg?style=flat-square)](VERSION.md)
[![Engine: Hindsight](https://img.shields.io/badge/Cognitive_Engine-Hindsight-6366F1.svg?style=flat-square)](docs/ai-memory/HINDSIGHT_INTEGRATION.md)
[![SOR: PostgreSQL](https://img.shields.io/badge/SOR-PostgreSQL_RLS-3B82F6.svg?style=flat-square)](docs/database/DATABASE_SCHEMA.md)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg?style=flat-square)](LICENSE)

*Investigate production outages using real-time telemetry and approved institutional memory recalled from previous incidents.*

</div>

---

## ⚡ The Problem: The "Amnesia Tax"

High-velocity engineering teams suffer from severe operational amnesia:
- **45% of production outages** are recurrences or slight variations of previously diagnosed failures.
- When critical alerts fire at 2 AM, on-call responders spend hours rediscovering solutions that were already thoroughly documented in forgotten postmortems.
- Generic AI chatbots hallucinate or blur concrete logs with unproven assumptions, risking catastrophic outages if responders act on ungrounded commands.

---

## 🚀 The Solution: OpsMemory AI

OpsMemory AI inverts this dynamic via persistent cognitive memory:

```
[ Incident Fires ] 
       │ 
       ▼
[ Multi-Modal Evidence Attached (Logs, Metrics, Diffs) ] 
       │ 
       ▼
[ Hindsight Associative Recall Queries Past Postmortems ] 
       │ 
       ▼
[ 5-Part Epistemological AI Investigation ] 
  ├── 1. Observed Facts (Verified Telemetry)
  ├── 2. Recalled Historical Memories (Precedent with Playbook Citation)
  ├── 3. Possible Root Causes (Evidence-Ranked Hypotheses)
  ├── 4. Recommended Safe Diagnostics (Read-Only Commands)
  └── 5. Unknown Information (Declared Telemetry Gaps)
       │ 
       ▼
[ Human Triage, Safe Inspection & Outage Mitigation ] 
       │ 
       ▼
[ Human-in-the-Loop Approval Queue (Rule BR-03) ] 
       │ 
       ▼
[ Hindsight Retain: Postmortem Committed to Institutional Memory ]
```

---

## 🌟 Key Features

- **Hindsight Long-Term Memory:** Uses official `retain`, `recall`, and `reflect` cognitive primitives with strict tenant bank isolation (`bank_id: org_{orgId}_ops`).
- **PostgreSQL as System of Record:** Canonical transactional storage with Row-Level Security (RLS) for incidents, evidence, postmortems, and immutable audit logs.
- **5-Part Epistemological Rigor:** Distinguishes observed facts from speculative root causes.
- **Non-Invasive Safety:** Suggests verified read-only inspection commands (`READ_ONLY_SAFE`); zero automated writes or destructive actions on live infrastructure.
- **Human-in-the-Loop Governance:** AI cannot commit claims to institutional memory without explicit Operations Admin approval.
- **Interactive Two-Incident Demo Studio:** Live interactive simulator demonstrating the complete memory reuse lifecycle from Incident 1 to Incident 2.
- **In-App Engineering Documentation Browser:** Live reader for all 14 project specifications across Phases 0 to 13.

---

## 🛠️ Tech Stack

- **Frontend:** React 19, TypeScript, Vite 6, Tailwind CSS v4, Lucide Icons.
- **Backend:** Node.js 22 LTS, Express, TypeScript, TSX.
- **Memory Engine:** Hindsight Cognitive Memory API (`vectorize-io/hindsight`) with resilient fallback.
- **System of Record:** PostgreSQL 16 Relational Schema with Row-Level Security.
- **Reasoning Agent:** Google Gemini API (`@google/genai`) with structured JSON schema validation.
- **Containerization:** Multi-stage Dockerfile and Docker Compose.

---

## 🏁 Quickstart

```bash
# 1. Clone repository & install dependencies
git clone https://github.com/opsmemory/opsmemory-ai.git
cd opsmemory-ai
npm install

# 2. Run deterministic unit tests (node:test)
npm run test

# 3. Start full-stack development server
npm run dev
# Open http://localhost:3000
```

---

## 🧪 Verification & Automated Testing

All core application logic is decoupled and tested with Node's built-in test runner:
```bash
npx --yes tsx --test src/services/engine.test.ts
```
**Test Results:**
- `✔ Retain: approved postmortem commits to Hindsight memory bank`
- `✔ Recall: querying incident symptoms returns relevant historical memory`
- `✔ Two-Incident E2E Journey: Incident 1 resolution directly informs Incident 2 investigation`
- `✔ Tenant Isolation: Tenant B cannot recall or query memories belonging to Tenant A`
- `✔ Epistemological Separation: AI investigation separates facts, memories, hypotheses, safe checks, and unknowns`
- `✔ Audit Service: records immutable audit events with actor and timestamp`

---

## 📖 Phase Documentation Directory

All phase-by-phase specifications are located under `/docs/` and accessible directly inside the web application:
- [Phase 0: Research & Reconnaissance](docs/research/)
- [Phase 1: Product Requirements](docs/product/)
- [Phase 2: Complete Architecture](docs/architecture/)
- [Phase 3: Database & API Contracts](docs/database/)
- [Phase 4: UI/UX Design System](docs/ui-ux/)
- [Phase 6: Hindsight Memory Engine](docs/ai-memory/)
- [Phase 7: AI Investigation Agent](docs/ai-agent/)
- [Phase 9: Security & Reliability](docs/security/)
- [Phase 10: Quality Assurance](docs/testing/)
- [Phase 11: Deployment & Production](docs/deployment/)
- [Phase 12: Hackathon Demo & Submission](docs/submission/)
- [Phase 13: Version Control & Status](IMPLEMENTATION_STATUS.md)

---

## 📄 License

Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE) for details.
