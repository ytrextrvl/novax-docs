
# Evidence Master (Owner-Friendly Verification)

## Production URLs (must work)
- Customer web: https://novaxtravel.com
- Customer web (www): https://www.novaxtravel.com
- Admin web: https://admin.novaxtravel.com
- API health: https://api.novaxtravel.com/health

## What to check (non-technical steps)
1) Open customer web and confirm home page loads (SSL lock icon present).
2) Open admin web and confirm login page loads; login works with a test admin user.
3) Open API health URL and confirm it returns OK.
4) Confirm latest deployments are healthy in Vercel and Render dashboards.
5) Confirm CI checks are green on the latest PR merges.

## Attach evidence
- Screenshots:
  - customer web home
  - admin login + dashboard
  - /health response
- Links:
  - Vercel deployments (web + admin)
  - Render service dashboard
  - CI run links
