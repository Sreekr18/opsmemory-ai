# Remediation Fix Plan: Phase B & Phase C Roadmaps

**Document Version:** 2.0.0  
**Phase:** Phase B (Prioritization & Execution Planning)  
**Date:** 2026-11-05  
**Owner:** Lead Auditor & Technical Documentation Owner  

---

## 1. Prioritization Matrix

All identified issues are ranked according to standard engineering severity and risk:

| Batch | Issue ID | Severity | Category | Risk Level | Description | Files to Modify |
|---|---|---|---|---|---|---|
| **Batch 1** | **SEC-001** | P1 | Security | Medium | Rate limiting middleware for AI endpoints | `server.ts` |
| **Batch 1** | **SEC-002** | P1 | Security | Low | Environment-aware auth token validation | `server.ts` |
| **Batch 2** | **PERF-001**| P2 | Performance| Low | LRU query cache in Hindsight memory | `src/services/hindsight.ts` |
| **Batch 2** | **API-001** | P2 | Feature | Low | Audit log export endpoint (JSON/CSV) | `server.ts`, `src/components/AuditLogsView.tsx` |
| **Batch 3** | **UX-001**  | P2 | UX | Very Low | "Clear Filters" button in Incidents Console | `src/components/IncidentsListView.tsx` |
| **Batch 3** | **UX-002**  | P3 | UX | Very Low | Hotkey support (Esc to close modals) | `src/App.tsx`, `GeminiCopilotView.tsx` |

---

## 2. Safe Execution Rules (Phase C)

1. **No Source Code Changes Without Approval:** Phase A is strictly read-only. Source code modifications are held until the user reviews and confirms Phase B.
2. **Small, Isolated Batches:** Changes will be applied in small atomic batches (Batch 1 -> Batch 2 -> Batch 3).
3. **Verification After Each Batch:**
   - Run `compile_applet` & `lint_applet`
   - Run `npm test`
   - Capture Playwright DOM snapshot to ensure zero regression.
4. **Preserve Working Code:** Ensure all existing capabilities, Two-Incident E2E Demo, and Gemini 3.8 Flash copilot continue to function flawlessly.
