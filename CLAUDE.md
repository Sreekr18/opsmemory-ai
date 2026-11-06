# Engineering Guidelines & Baseline Protocol: OpsMemory AI

This document establishes the mandatory engineering standards, discipline, and operational practices for developing, auditing, maintaining, and scaling the OpsMemory AI platform.

---

## 1. THINK BEFORE CODING
- Read and understand the existing project thoroughly before making changes.
- Inspect the folder structure, source files, dependencies, database schema, APIs, and current functionality.
- Identify assumptions, missing requirements, and technical conflicts.
- Never silently invent requirements.
- Ask questions when critical information is missing.
- Present a brief implementation plan before complex changes.

---

## 2. SIMPLICITY FIRST
- Implement the simplest reliable solution.
- Avoid unnecessary dependencies and packages.
- Avoid duplicate components, APIs, services, and database models.
- Do not introduce speculative features.
- Avoid overengineering and unnecessary abstractions.
- Follow the existing framework and coding conventions.

---

## 3. SURGICAL CHANGES
- Preserve all existing working features.
- Modify only the files required for the requested task.
- Do not replace the entire application unnecessarily.
- Do not delete existing functionality without explicit approval.
- Maintain existing API contracts and database compatibility.
- Avoid breaking changes.
- Clean up only unused code introduced by your own changes.

---

## 4. GOAL-DRIVEN EXECUTION
Every task must have:
1. Clearly defined objective.
2. Implementation plan.
3. Success criteria.
4. Implementation.
5. Testing.
6. Verification.
7. Final implementation report.

Continue improving the implementation until the defined success criteria are met or a genuine blocker is identified.

---

## 5. PROJECT UNDERSTANDING
Before implementation, inspect:
- Frontend architecture (React 19, Tailwind CSS v4, Motion).
- Backend architecture (Express, Node.js 22 LTS, TypeScript).
- Database and relationships (PostgreSQL 16 System of Record, in-memory store simulation, RLS).
- Authentication and authorization (RBAC: `OPERATIONS_ADMIN`, `DEVOPS_ENGINEER`, `ORGANIZATION_OWNER`).
- API endpoints (`/api/incidents`, `/api/gemini/chat`, `/api/memory/*`, `/api/audit-logs/*`).
- UI components and design system (Google Stitch & Gemini AI obsidian aesthetics).
- Existing features and user workflows (Two-Incident E2E Demo, Epistemological separation, WORM audit trail).
- Environment configuration (`.env.example`, `GEMINI_API_KEY`).
- Error handling and logging.
- Existing tests (`src/services/engine.test.ts`).

Do not assume a feature is missing before checking the existing code.

---

## 6. SECURITY REQUIREMENTS
- Never expose API keys, credentials, or secrets in frontend bundles or Git.
- Validate and sanitize all user inputs.
- Implement proper authentication and authorization.
- Enforce server-side permissions and tenant memory bank isolation (`Rule BR-08`).
- Prevent unauthorized cross-tenant data access.
- Protect sensitive API endpoints with rate limiting (`SEC-001`).
- Never trust frontend-only validation.
- Follow secure database and session practices.
- Enforce non-destructive operations: only safe, read-only diagnostic commands allowed (`Rule BR-07`).

---

## 7. UI/UX REQUIREMENTS
- Preserve the existing design language (Google Stitch & Gemini AI).
- Maintain responsive layouts across desktop (1440x900) and mobile (390x844).
- Ensure accessible interactions and semantic HTML.
- Handle loading, empty, error, and success states cleanly.
- Avoid unnecessary redesigns.
- Maintain consistent typography, spacing, and component hierarchy.

---

## 8. DATABASE AND API REQUIREMENTS
- Inspect the existing schema before changing it.
- Preserve data integrity and foreign key relationships.
- Avoid duplicate database records via deterministic deduplication hashes.
- Use proper validation and RFC 7807 error responses.
- Maintain backward API compatibility.
- Provide migrations when schema changes are necessary.
- Never silently delete production data.

---

## 9. TESTING AND VERIFICATION
For every significant change:
- Run relevant unit tests (`npx --yes tsx --test src/services/engine.test.ts`).
- Check build and compilation (`compile_applet`).
- Check TypeScript types and linting (`tsc --noEmit` via `lint_applet`).
- Check API functionality via curl / fetch.
- Check database operations and tenant isolation.
- Check existing feature regression.
- Check authentication and authorization.
- Report failures honestly.
- Never claim that something was tested, executed, or verified unless it actually was.
- If execution is unavailable, clearly label the result as `NOT VERIFIED`.

---

## 10. CHANGE REPORTING VOCABULARY
Use only these standardized implementation statuses:
- `IMPLEMENTED`
- `TESTED`
- `VERIFIED`
- `BLOCKED`
- `NOT IMPLEMENTED`
- `NOT VERIFIED`

---

## 11. IMPORTANT RULES
- Never fabricate functionality.
- Never create fake API responses to simulate completed backend functionality.
- Never replace real database operations with dummy data without permission.
- Never hide errors.
- Never sacrifice security for convenience.
- Never claim completion without evidence.
- Prioritize correctness, maintainability, security, and simplicity.
