# Bug & Defect Register: OpsMemory AI

**Document Version:** 2.0.0  
**Phase:** Phase A (System Audit)  
**Date:** 2026-11-05  

---

## 1. Summary of Identified Defects

| Bug ID | Title | Severity | Module | Status |
|---|---|---|---|---|
| **BUG-001** | Missing Rate Limiting on AI Generation Endpoints | P1 (High) | `server.ts` | IDENTIFIED |
| **BUG-002** | Implicit Tenant Context Ingestion When Headers Missing | P1 (High) | `server.ts` | IDENTIFIED |
| **BUG-003** | Lack of Explicit Empty State Reset in Incident Filter | P2 (Medium) | `IncidentsListView.tsx` | IDENTIFIED |
| **BUG-004** | Missing Compliance Export for Audit Trail | P2 (Medium) | `AuditLogsView.tsx` | IDENTIFIED |
| **BUG-005** | Memory Bank Cache Unbounded Growth Under Sustained Queries | P2 (Medium) | `src/services/hindsight.ts` | IDENTIFIED |
| **BUG-006** | Keyboard Escape Handler Missing on Gemini Copilot Input | P3 (Low) | `GeminiCopilotView.tsx` | IDENTIFIED |

---

## 2. Detailed Bug Profiles

### BUG-001: Missing Rate Limiting on AI Generation Endpoints
- **Severity:** P1 (High)
- **Affected Module:** `server.ts` (`/api/gemini/chat`, `/api/incidents/:id/investigate`)
- **Reproduction Steps:**
  1. Fire rapid consecutive POST requests to `http://localhost:3000/api/gemini/chat`.
  2. Observe that every request is processed immediately without HTTP 429 throttling.
- **Expected Behavior:** Endpoint should throttle requests exceeding 30 requests/minute per IP/tenant and respond with HTTP 429 (`Too Many Requests`).
- **Actual Behavior:** Unrestricted access permits potential API quota exhaustion or server load spikes.
- **Root Cause:** No rate limiting middleware configured in Express pipeline.

---

### BUG-002: Implicit Tenant Context Ingestion
- **Severity:** P1 (High)
- **Affected Module:** `server.ts` (`app.use` middleware)
- **Reproduction Steps:**
  1. Send request without `x-organization-id` or `Authorization` headers.
  2. Server defaults to `org_acme_prod` and `usr_marcus`.
- **Expected Behavior:** In production mode (`NODE_ENV === 'production'`), requests missing tenant credentials must be rejected with HTTP 401 Unauthorized.
- **Actual Behavior:** Development fallback currently applies indiscriminately.
- **Root Cause:** Missing check for `process.env.NODE_ENV === 'production'` in tenant context resolver.

---

### BUG-003: Incident Filter Empty State UX
- **Severity:** P2 (Medium)
- **Affected Module:** `src/components/IncidentsListView.tsx`
- **Reproduction Steps:**
  1. Select a filter combination that yields 0 matching incidents (e.g. SEV-4 + Mitigated).
  2. Empty state shows "No incidents match your filter" but does not offer a 1-click "Clear Filters" button.
- **Expected Behavior:** An actionable button allows the user to immediately reset active filters.
- **Actual Behavior:** User must manually deselect each dropdown option.

---

### BUG-004: Audit Trail Compliance Export Missing
- **Severity:** P2 (Medium)
- **Affected Module:** `server.ts` & `src/components/AuditLogsView.tsx`
- **Reproduction Steps:**
  1. Navigate to "Security & Audit Logs".
  2. Notice no button to export audit records to JSON or CSV for external compliance auditors (SOC 2 / ISO 27001).
- **Expected Behavior:** Standard SaaS compliance requirement to export signed audit events.

---

### BUG-005: Unbounded Hindsight Cache
- **Severity:** P2 (Medium)
- **Affected Module:** `src/services/hindsight.ts`
- **Reproduction Steps:**
  1. Execute thousands of distinct test queries through `hindsight.recall()`.
  2. Local memory structures grow proportionally without an LRU maximum cache limit.
- **Expected Behavior:** Memory cache should enforce a maximum size (e.g., 500 entries) with least-recently-used eviction.
