# Regression Analysis & Safety Matrix: OpsMemory AI

**Document Version:** 2.0.0  
**Phase:** Phase A  
**Date:** 2026-11-05  
**Engineer:** Senior Quality Assurance & Regression Specialist  

---

## 1. Regression Risk Assessment

Before making any code modifications in subsequent remediation phases, this matrix documents the baseline functionality that must remain 100% operational with zero regression:

| Core Functional Area | Critical Validation Requirement | Regression Risk | Regression Test Method |
|---|---|---|---|
| **Hindsight Retain & Recall** | Approved postmortem stored in bank and retrievable via cosine similarity | High | `npm test` test 1 & 2 |
| **Two-Incident Journey** | Incident 1 postmortem changes Incident 2 investigation confidence and MTTR | High | `npm test` test 3 & UI Simulation |
| **Tenant Isolation** | Tenant B receives 0 memories from Tenant A | High | `npm test` test 4 |
| **Epistemological Separation** | Hypotheses and safe commands are never converted into hard facts | High | `npm test` test 5 |
| **Gemini 3.8 Flash Chat** | Grounded chat responds in <4s with Hindsight citation chips | Medium | `POST /api/gemini/chat` curl & UI |
| **Audit Log Trail** | All state mutations append immutable audit event | Medium | `npm test` test 6 |
| **Responsive UI & Mobile Bar**| Mobile navigation maintains 44px touch targets without horizontal scroll | Low | Playwright mobile snapshot |

---

## 2. Regression Defense Protocol

1. **Pre-Change Baseline Verification:** All tests must pass prior to modifying code.
2. **Atomic Commits / Edits:** Edits are restricted to targeted lines using `replace_file_content`.
3. **Post-Change Verification:** Immediate co-execution of `compile_applet`, `lint_applet`, and `npm test`.
4. **Visual Regression:** Playwright snapshot comparison on key user flows.
