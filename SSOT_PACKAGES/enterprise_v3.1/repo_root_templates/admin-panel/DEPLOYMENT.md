# Deployment

## Staging
- Deployment method:
- Environment variables location:
- Verification steps:

## Production
- Deployment method:
- Rollback steps:
  - Vercel: rollback to previous deployment
  - Render: redeploy last-known-good
  - DB: rollback only via explicit migration rollback plan

## Health
- /health must return OK
