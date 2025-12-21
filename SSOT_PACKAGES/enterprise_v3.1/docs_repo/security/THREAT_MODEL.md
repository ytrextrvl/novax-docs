
# Threat Model (Baseline)

## Assets
- User identities, sessions, PII
- Admin credentials and privileges
- Wallet balances and loyalty points
- Payments, refunds, settlements
- Booking lifecycle states and issuance data
- API keys and provider credentials (stored only in secret managers)

## Entry points
- Public API endpoints (`/v1/*`)
- Admin UI
- Customer web UI
- Mobile app
- CI/CD pipelines

## Key threats and mitigations (minimum)
1) Credential stuffing / account takeover
   - Rate limiting, bot protection, MFA/OTP for high-risk actions, suspicious login alerts.
2) Privilege escalation in Admin
   - Strict RBAC enforcement on server; CODEOWNERS + reviews for RBAC changes; audit logs.
3) Payment replay / double charge
   - Idempotency keys + replay protection + transaction logs.
4) Injection / SSRF
   - Input validation, safe HTTP clients, allowlists, parameterized queries.
5) Data exfiltration
   - Least privilege DB user, strict storage ACLs, log redaction, WAF rules.
6) Supply chain compromise
   - Dependency scanning, lockfiles, CI protections, signed releases (recommended).

## Security acceptance
- WAF + rate limits enabled
- Secrets never committed
- Audit logs present and queryable
