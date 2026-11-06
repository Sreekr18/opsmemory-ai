# Contributing to OpsMemory AI

**Product:** OpsMemory AI  
**Baseline Version:** 0.1.0  
**Phase:** 13 — Version Control & Change Management  
**Status:** VERIFIED  

---

## 1. Engineering Principles & Clean-Room Standards

Thank you for contributing to OpsMemory AI! As an enterprise-grade SRE platform, we maintain strict engineering and legal hygiene:

1. **Clean-Room Engineering:** Do not copy or adapt source code from copyleft (GPL/AGPL) or source-available/proprietary projects (BSL/SSPL). Only use permissive MIT or Apache 2.0 reference implementations.
2. **PostgreSQL as System of Record:** Never bypass PostgreSQL transactional storage for state updates.
3. **No Unverified Claims:** Do not claim a feature or test is verified without running the verification suite and documenting actual output evidence.
4. **Epistemological Integrity:** Any change to the Investigation Agent must uphold the 5-part epistemological contract.

---

## 2. Development & Testing Workflow

```bash
# 1. Install dependencies
npm install

# 2. Run deterministic unit test suite (Node built-in runner)
npm run test
# or: npx --yes tsx --test src/services/engine.test.ts

# 3. Check TypeScript compilation & linting
npm run lint

# 4. Start local development server
npm run dev
```

---

## 3. Pull Request Guidelines

Every Pull Request must include:
- Description of the change and reason.
- Impact on tenant boundary isolation and memory retention.
- Terminal output of `npm run test` demonstrating that all assertions pass.
- Updates to `CHANGELOG.md` and `IMPLEMENTATION_STATUS.md`.
