
# Operations Runbooks

## 1) DNS & SSL (Cloudflare)
- SSL mode: Full (Strict)
- Enable WAF managed rules
- Add rate limits for:
  - /v1/auth/*
  - /v1/payments/*
  - /v1/bookings/*
- DNS:
  - apex + www -> Vercel (Customer web)
  - admin -> Vercel (Admin)
  - api -> Render (Backend)

## 2) Render (Backend)
- Health check path: /health
- Configure environment variables from secrets only
- Enable logs and error alerting

## 3) Vercel (Web/Admin)
- Separate projects for web and admin
- Map domains and configure environment variables
- Ensure previews on PR and production on merge

## 4) Neon (DB)
- Least privilege app user
- Controlled migrations (CI gate)
- Backups/PITR enabled if available

## 5) Incident response (minimum)
- SEV1: major outage / payment failure
- SEV2: partial outage
- SEV3: degraded performance
- SEV4: minor issue
Steps: Detect -> Mitigate -> Communicate -> RCA -> Prevent
