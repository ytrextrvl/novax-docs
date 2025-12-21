
# Risk Register (Baseline)

| ID | Risk | Impact | Likelihood | Mitigation | Owner |
|---|------|--------|------------|------------|-------|
| R-001 | Secrets committed to Git | Critical | Medium | Secret scanning + PR checks + training | Security |
| R-002 | Payment double-charge | Critical | Low/Med | Idempotency keys + audits + monitoring | Backend/Finance |
| R-003 | Broken deploy via main push | High | Medium | Branch protection + required checks | DevOps |
| R-004 | Data loss | Critical | Low/Med | Backups + PITR + DR testing | DevOps |
| R-005 | RBAC misconfig | High | Medium | RBAC matrix + tests + CODEOWNERS | Security |
