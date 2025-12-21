
# Release & Change Management

## Release types
- Patch: bug fix
- Minor: new features (backward compatible)
- Major: breaking changes

## Workflow
1) PR approved + CI green
2) Update changelog and evidence
3) Deploy (Render/Vercel)
4) Post-deploy verification using Evidence Master
5) Tag release (recommended)

## Rollback
- Vercel: rollback to previous deployment
- Render: rollback to previous image/build or redeploy last-known-good
- DB: rollback migrations only via explicit rollback plan
