
# GitHub Governance (Enterprise Baseline)

## Branch protection (mandatory)
Apply to `main` on all repos:
- Require pull request reviews (minimum 1)
- Require status checks to pass before merging
- Require branches to be up to date before merging
- Restrict who can push to matching branches (no direct pushes)
- Dismiss stale reviews on new commits
- Require signed commits (recommended)

## Required checks (minimum)
- Lint
- Tests (unit + critical integration where available)
- Build

## PR policy
- PR title format: `NOVAX:<Repo>: <Short change>`
- PR body must include:
  - What changed
  - Risk assessment
  - Rollback plan
  - Evidence (CI links + screenshots/URLs where applicable)

## Secrets policy
- No secrets in repo history.
- Use GitHub Secrets for CI; Vercel/Render/Neon/Cloudflare for runtime secrets.
- Only commit `.env.example`.

## CODEOWNERS
- CODEOWNERS is mandatory to enforce approvals for sensitive areas:
  - security/
  - payments/
  - infrastructure/
  - migrations/
