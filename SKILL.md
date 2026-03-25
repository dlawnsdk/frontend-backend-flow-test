---
name: frontend-backend-flow-test
description: Analyze frontend API usage, compare it with backend contracts, and optionally run transaction-style live API tests with best-effort cleanup. Use when validating whether web/mobile/admin frontend requests are correctly accepted by backend endpoints, DTOs, auth rules, and response shapes. Best for frontend-backend contract validation, regression auditing, and controlled real-data verification in dev/staging environments. NOT for: production write testing, guaranteed rollback, or fully automatic support for arbitrary APIs without configuration.
---

# Frontend-Backend Flow Test

Analyze frontend API usage, compare it with backend contracts, and optionally run transaction-style live API tests with best-effort cleanup.

**⚠️ Beta (v1.2.0)**
- Audit mode is the default and safest mode
- Live mode is opt-in
- Dev/staging only for write tests
- Cleanup is best-effort, not true rollback
- Side effects may remain after live tests

See [README.md](README.md) for maturity notes and [LIMITATIONS.md](references/LIMITATIONS.md) for operational constraints.

## Overview

This skill is designed to verify whether frontend request flows are actually compatible with backend API contracts.

It works in two layers:

### 1. Audit mode (default)
- Analyze frontend API calls from web, mobile, or admin code
- Extract request method, path, headers, query, body shape, and response field usage
- Compare them against backend controllers, DTOs, auth requirements, and response structures
- Produce mismatch notes and validation reports

### 2. Live mode (optional)
- Execute selected API scenarios against a real environment
- Validate request/response behavior with real data
- Run transaction-style test flows when configured
- Attempt best-effort cleanup after test execution

## What it does well

- Analyze frontend API usage patterns
- Compare frontend expectations with backend endpoint contracts
- Detect method/path/payload/auth/response mismatches
- Help audit regressions across web/mobile/admin surfaces
- Optionally run controlled live API checks in dev/staging
- Attempt cleanup-oriented validation flows after write tests

## What it does NOT do

- Guaranteed rollback across side effects
- Production-safe write testing
- Full browser/app UI automation
- Comprehensive QA replacement
- Fully automatic support for arbitrary APIs without configuration

## Modes

### Audit mode
Default mode.

Use this mode when you want static analysis only:
- no real write requests
- no live data mutation
- contract mismatch reporting only

### Live read-only mode
Optional.

Use this mode when you want to verify safe request/response behavior against a real environment without write operations.

### Live write mode
Optional.

Use this mode when you want create/update/delete validation with best-effort cleanup.
Use only in isolated dev/staging environments.

## Typical workflow

1. Inspect frontend API call sites
2. Extract request method, path, auth, query, and payload usage
3. Inspect backend controller mappings and DTO contracts
4. Compare frontend expectations against backend definitions
5. Summarize mismatches and likely breakpoints
6. Optionally run live verification scenarios
7. Attempt best-effort cleanup for write scenarios

## Suggested outputs

This skill may produce:
- frontend-backend contract audit reports
- endpoint mismatch summaries
- auth/DTO/response compatibility notes
- optional live transaction-style test results
- cleanup result summaries

## When to use

Use this skill when:
- frontend and backend evolve separately
- you want to catch request/response contract mismatches early
- you want optional real-data verification in dev/staging
- you need regression auditing across multiple frontend surfaces

## Safety rules

- Default to audit mode unless live testing is explicitly appropriate
- Treat live write tests as opt-in only
- Never assume cleanup is equivalent to DB transaction rollback
- Warn clearly when side effects may survive cleanup
- Do not position live mode as production-safe

## References

Read these when needed:
- [CONFIG.md](references/CONFIG.md) for configuration direction
- [LIMITATIONS.md](references/LIMITATIONS.md) for scope and safety limits
- [EXAMPLES.md](references/EXAMPLES.md) for example scenarios
