
# Data Retention & Privacy (Baseline)

## Classification
- Public: marketing content
- Internal: operational metadata
- Sensitive: PII (names, phone, email), booking references
- Restricted: auth secrets, tokens, payment-related secrets

## Baseline retention (adjust per policy)
- Audit logs: 24 months
- Operational logs: 30-90 days
- Payment ledger: per legal/business retention (recommended 5+ years)
- PII deletion: define procedure (export/delete) if required by policy

## Access control
- PII access limited to Support/Operations with audit trail.
- Exports require approval; export events audited.
