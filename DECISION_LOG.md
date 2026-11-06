# Architectural Decision Log (ADR Summary)

**Product:** OpsMemory AI  
**Baseline Version:** 0.1.0  
**Phase:** 13 — Version Control & Change Management  
**Status:** VERIFIED  

---

## 1. Architectural Decision Records (ADR Index)

### ADR-001: Separation of Transactional Record and Cognitive Memory
- **Date:** 2026-11-04
- **Status:** ACCEPTED
- **Context:** SRE operations require ACID durability for incident status transitions, evidence timestamps, and compliance audits, whereas cognitive memory requires semantic associative graphs.
- **Decision:** PostgreSQL is the application's transactional system of record. Hindsight is the cognitive long-term memory engine. Hindsight outages must never block PostgreSQL writes.

### ADR-002: Strict Multi-Tenant Memory Bank Partitioning
- **Date:** 2026-11-04
- **Status:** ACCEPTED
- **Context:** In multi-tenant B2B SaaS, customer A must never recall postmortems or evidence belonging to customer B.
- **Decision:** Memory bank IDs strictly follow `bank_id = org_{orgId}_ops`. The backend injects the tenant ID server-side; cross-bank queries are prevented at the protocol layer.

### ADR-003: 5-Part Epistemological Investigation Contract
- **Date:** 2026-11-04
- **Status:** ACCEPTED
- **Context:** Generic LLM chatbots blur concrete logs with speculative root causes, risking catastrophic outages if on-call responders act on hallucinations.
- **Decision:** Every AI investigation report strictly isolates:
  1. `observed_facts` (grounded in attached telemetry)
  2. `historical_memories` (recalled past postmortems)
  3. `possible_root_causes` (ranked hypotheses with evidence citations)
  4. `recommended_diagnostic_checks` (read-only safe commands)
  5. `unknown_information` (unprobed parameters)

### ADR-004: Mandatory Human-in-the-Loop Knowledge Approval
- **Date:** 2026-11-04
- **Status:** ACCEPTED
- **Context:** Automatically committing AI-generated claims to long-term organizational memory risks poisoning future investigations with false assumptions.
- **Decision:** Rule BR-03 enforces that postmortems must be reviewed and approved by an `OPERATIONS_ADMIN` or `ORGANIZATION_OWNER` before calling Hindsight `retain()`.

### ADR-005: Read-Only Tool Execution Boundary (Zero Autonomous Mutations)
- **Date:** 2026-11-04
- **Status:** ACCEPTED
- **Context:** Autonomous execution of remediation commands on production clusters carries unacceptable operational risk.
- **Decision:** OpsMemory AI recommends safe read-only diagnostics (`SELECT * FROM pg_stat_activity`, `kubectl logs`), but never executes automated writes or modifications against production infrastructure.

### ADR-006: Deterministic Local Cognitive Fallback for Hindsight
- **Date:** 2026-11-04
- **Status:** ACCEPTED
- **Context:** If the external Hindsight cluster or network is disrupted, incident responders must not be left without triage capabilities.
- **Decision:** The Hindsight client implements a circuit breaker and fallback adapter with local token-weighted associative matching, ensuring 100% platform availability.
