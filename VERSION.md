# Product Version Specification

**Product:** OpsMemory AI  
**Current Baseline Version:** 0.2.1  
**Release Type:** MINOR (Alert Webhook Gateway & ChatOps Slack Integration)  
**Release Date:** 2026-11-05  
**Release Target:** Enterprise B2B SaaS Release / Hackathon Final Submission  

---

## Semantic Versioning Rules

OpsMemory AI strictly follows Semantic Versioning (SemVer 2.0.0):
- **MAJOR (X.y.z):** Breaking API schema changes, backward-incompatible database migrations, or core memory engine protocol revisions.
- **MINOR (x.Y.z):** New backward-compatible operational capabilities, additional evidence types, or new integrations.
- **PATCH (x.y.Z):** Backward-compatible bug fixes, UI polish, and performance optimizations.

---

## Active Component Versions

| Component | Target Version | Engine / Runtime | Status |
|---|---|---|---|
| **Core API Service** | `0.2.0` | Node.js 22 LTS / Express / TypeScript (Rate Limited & Auth Guarded) | VERIFIED |
| **System of Record (SOR)** | `0.1.0` | PostgreSQL 16 Relational Schema with RLS | VERIFIED |
| **Hindsight Memory Adapter** | `0.2.0` | Hindsight v0.2.x REST / Bounded LRU Cache (PERF-001) | VERIFIED |
| **Gemini Ops Intelligence** | `0.2.0` | Gemini 3.8 Flash via `@google/genai` with 4s Timeout | VERIFIED |
| **Operations Web Console** | `0.2.0` | React 19 / Vite 6 / Tailwind CSS v4 / Audit Export & Empty State | VERIFIED |
