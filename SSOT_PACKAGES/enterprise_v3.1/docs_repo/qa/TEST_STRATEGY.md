
# Test Strategy (Enterprise Baseline)

## Backend
- Unit tests for:
  - Pricing rules
  - Booking state machine
  - Wallet/ledger invariants
- Integration tests for:
  - Auth + RBAC enforcement
  - Booking create + payment idempotency
- Contract tests:
  - Validate endpoints match OpenAPI (schema)

## Web/Admin
- Build and typecheck required
- Smoke test critical routes (login, search, booking, admin dashboard)

## Mobile
- Analyze required
- Build artifacts required
- Smoke tests for offline sync (as available)

## Quality gates
- No merge with failing lint/tests/build.
