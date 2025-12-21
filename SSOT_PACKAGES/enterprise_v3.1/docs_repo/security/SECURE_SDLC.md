
# Secure SDLC (Baseline)

## Mandatory controls
- PR-only workflow and branch protection
- CODEOWNERS for security-sensitive paths
- Dependency scanning (Dependabot or equivalent)
- Secrets scanning (prevent secrets in commits)
- CI required checks before merge

## Change classes
- Low risk: docs, UI copy, non-sensitive refactors
- Medium risk: API changes, migrations, pricing rules
- High risk: auth/RBAC, payments, secrets/infra, migrations touching financial data

## High risk change requirements
- Explicit rollback plan
- 2 approvals (including security/finance owner)
- Evidence update in EVIDENCE_MASTER
