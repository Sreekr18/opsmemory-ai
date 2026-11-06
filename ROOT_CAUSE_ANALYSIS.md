# Root Cause Analysis: Systemic Audit Findings

**Document Version:** 2.0.0  
**Phase:** Phase A  
**Date:** 2026-11-05  
**Author:** Lead Systems Architect & Independent Verification Engineer  

---

## 1. Systemic Issue Catalog

### RCA-001: Missing Request Throttling on AI Endpoints
- **Symptom:** Concurrent automated requests can trigger unmetered LLM queries.
- **Root Cause:** Express server pipeline lacked a rate-limiting middleware filter before hitting generative endpoints.
- **Remediation Strategy:** Introduce an in-memory token bucket rate limiter in `server.ts` that limits clients to 30 requests per minute per IP, responding with HTTP 429 when breached.

---

### RCA-002: Development Fallback for Unauthenticated Requests
- **Symptom:** Requests without authorization headers automatically authenticate as `usr_marcus` / `org_acme_prod`.
- **Root Cause:** Middleware was authored with developer ergonomics as default to enable local testing without login tokens.
- **Remediation Strategy:** Conditionally enforce strict token verification when `process.env.NODE_ENV === 'production'`, returning HTTP 401 for unauthenticated calls while preserving safe local ergonomics in dev.

---

### RCA-003: Unbounded In-Memory Query Cache in Hindsight
- **Symptom:** Long-running node processes with high search throughput retain all query embeddings indefinitely.
- **Root Cause:** Javascript `Map` was used as a query cache without max size eviction logic.
- **Remediation Strategy:** Implement an LRU cache eviction policy with a fixed ceiling (e.g. 500 entries).

---

### RCA-004: Lack of "Clear Filters" in Incident Console
- **Symptom:** When filtering by severity and status yields 0 results, the user has to click each dropdown individually to reset.
- **Root Cause:** `IncidentsListView.tsx` only had an empty text message and did not render a reset action button.
- **Remediation Strategy:** Add a 1-click "Reset All Filters" button inside the empty state component.

---

### RCA-005: Audit Log Export Missing
- **Symptom:** Responders and compliance teams cannot download audit logs as CSV or JSON.
- **Root Cause:** Store had `listAuditLogs()` but no serialization export helper or UI export trigger.
- **Remediation Strategy:** Add `GET /api/audit-logs/export?format=json|csv` and a download button in `AuditLogsView.tsx`.
