
# Data Model Overview (Baseline)

## Core aggregates
- Users, Roles, Permissions
- Agents, Companies
- Bookings (state machine)
- Payments, Refunds
- Wallet transactions (ledger)
- Loyalty transactions
- Pricing rules
- Audit logs

## Invariants (must hold)
- Ledger must balance (no negative wallet without explicit overdraft policy).
- Booking state transitions must be valid and audited.
- Financial actions must be idempotent and auditable.
