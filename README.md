# Frontend-Backend Flow Test

## Maturity Level: **Beta (7.0/10)**

---

## What This Skill Is

Frontend-Backend Flow Test analyzes frontend API usage, compares it with backend contracts, and can optionally run transaction-style live API tests with best-effort cleanup.

This is **not** just a CRUD generator anymore.
The primary value is:

1. **Contract audit** — verify that frontend request flows match backend endpoint contracts
2. **Optional live verification** — run selected real-data scenarios in dev/staging
3. **Best-effort cleanup** — attempt cleanup after write tests, without claiming true rollback

---

## Core Modes

### 1. Audit mode (default)
Use when you want static verification only.

Checks may include:
- frontend request method/path usage
- header/auth expectations
- request payload shape
- query parameter usage
- response field usage
- backend controller / DTO alignment

### 2. Live read-only mode
Use when you want real-environment verification without write operations.

### 3. Live write mode
Use when you want controlled create/update/delete validation with cleanup attempts.

**Important:** cleanup is best-effort only. Side effects may remain.

---

## Good Fit

- Frontend-backend contract validation
- Regression auditing across web/mobile/admin
- Controlled dev/staging real-data verification
- API flow sanity checks before release
- Detecting request/response drift between frontend and backend

## Not a Good Fit

- Production write testing
- Guaranteed rollback requirements
- Full browser/app UI automation
- Comprehensive QA replacement
- Arbitrary APIs with zero configuration

---

## Strengths

- Clear split between audit mode and live mode
- Better fit for real frontend-backend integration work
- Useful for multi-surface products like web/mobile/admin stacks
- Safer positioning than generic “automatic rollback” tooling
- Flexible path toward contract reports + live validation

---

## Current Limitations

### Audit limitations
- Contract extraction still depends on recognizable frontend/backend patterns
- Dynamic request assembly may be hard to infer automatically
- Response usage analysis may miss indirect or computed usage

### Live test limitations
- Cleanup is **not** true transaction rollback
- Side effects may remain (emails, notifications, webhooks, logs, external integrations)
- Production-safe write verification is not supported
- Environment-specific auth and payload rules still need configuration

### Test quality limitations
- Live checks should be positioned as targeted validation, not full QA coverage
- Schema validation, richer field assertions, and dependency-aware cleanup may require future expansion

---

## Recommended Roadmap

### High Priority
1. Add frontend request extraction patterns for Flutter/React-style API layers
2. Add backend contract extraction patterns for Spring controllers/DTOs
3. Define contract mismatch report format
4. Add live-mode configuration schema
5. Add stronger safety gates for write tests

### Medium Priority
6. Add request encoding options (`json`, `data`, `params`, multipart)
7. Add configurable auth extraction flows
8. Add field-level assertion options
9. Add dependency-aware cleanup strategies
10. Add retry support for eventual consistency

### Low Priority
11. Add reusable report templates
12. Add surface-specific examples (mobile/web/admin)
13. Add CI-oriented audit output modes
14. Add richer environment policy controls

---

## User Guidance

Before using this skill:
1. Decide whether audit mode alone is enough
2. Use live mode only when real API verification is actually needed
3. Keep write tests in isolated dev/staging environments
4. Assume cleanup may be incomplete
5. Treat reports as contract validation evidence, not production safety guarantees

---

## Summary

**Use this skill when:**
- you want to verify whether frontend request flows match backend contracts
- you want optional live validation with controlled real-data scenarios
- you need regression auditing across frontend and backend surfaces

**Do not use this skill when:**
- production write safety is required
- guaranteed rollback is required
- full E2E automation is expected

---

**Version:** 1.2.0  
**Status:** Beta / Repositioned Scope  
**Maintainer:** @dlawnsdk
