
# Architecture (Enterprise Overview)

## Topology
- Edge: Cloudflare (DNS, SSL Full (Strict), WAF, Rate limiting)
- Backend: Render (Laravel API)
- Frontends: Vercel (Customer Web, Admin Web)
- Database: Neon PostgreSQL
- Storage: Backblaze B2 (S3-compatible)
- Push: Firebase Cloud Messaging (FCM)

## Core principles
- API-first; contract-driven via OpenAPI.
- RBAC enforced server-side; deny-by-default.
- Evidence-based releases: do not claim “done” without URLs + verification steps.
- Observability-first: structured logs, correlation IDs, audit logs.

## Required health endpoints
- GET /health  -> OK (and minimal dependency status)
- Optional: GET /ready, GET /live
