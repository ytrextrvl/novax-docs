# NOVAX TRAVEL — SOURCE OF TRUTH (SSoT)

> هذا الملف مولّد آلياً من وثيقة DOCX الرسمية، بهدف تحويلها إلى Markdown قابل للتنفيذ داخل GitHub.
> Generated: 2025-12-21 00:47:08Z

---

وثيقة توصيف مشروع NOVAX TRAVEL

Project Description & Requirements Specification (Arabic-first)

الإصدار: 1.0
التاريخ: 2025-12-18
الغرض: توصيف شامل للمشروع (ليست وثيقة أمر تنفيذ)


# 1. مقدمة وتعريف بالمشروع

NOVAX TRAVEL هو مشروع منصة سفر وحجوزات متعددة القنوات (موقع العملاء + لوحة إدارة + تطبيق جوال + API) تهدف إلى توفير تجربة حجز احترافية بمستوى عالمي مع جاهزية تشغيل فعلية في بيئة إنتاج خارجية. هذه الوثيقة هي توصيف شامل للمشروع ومتطلباته الوظيفية وغير الوظيفية، وليست أمرًا بالتنفيذ.

## 1.1 نطاق هذه الوثيقة

- توصيف الغرض والنتائج المتوقعة من المنصة.

- تحديد المكونات الرئيسية (Backend/Web/Admin/Mobile/Infra).

- توثيق متطلبات الاستضافة والمزودين والبنية التحتية.

- توثيق متطلبات الأمان والحوكمة وإدارة الصلاحيات.

- تحديد معايير التحقق (Definition of Done) كمرجع قبول.

- فهرس مرجعي للفصول التفصيلية كما وردت في المصدر الأصلي.

## 1.2 تعريفات مختصرة

- Web: موقع العملاء (واجهة الحجز والخدمات).

- Admin: لوحة التحكم والإدارة والعمليات.

- API/Backend: خدمات الخلفية (Business Logic) وقواعد البيانات والتكاملات.

- Infra: البنية التحتية (DNS/SSL/WAF/Hosting/CI-CD/Monitoring).

- Environments: بيئات التشغيل (Staging/Production).

# 2. أهداف المشروع

- تقديم منصة حجز سفر متكاملة (Flights/Hotels/Cars/Visas وخدمات تشغيلية مرتبطة).

- تجربة استخدام سريعة وواضحة وآمنة (Trust, Speed, Clarity, Security).

- لوحة إدارة شاملة لإدارة البيانات والعمليات والصلاحيات والمالية والتقارير.

- جاهزية تشغيل إنتاجية (Production-ready) مع مراقبة وصحة خدمة /health وحماية طبقة الشبكة.

- قابلية توسع دولي مع تركيز بيانات اليمن كبداية (مدن/محافظات/مسارات/شركات طيران محلية).

# 3. مكونات النظام وحدود المسؤوليات

## 3.1 المكونات الأساسية

- Backend API: إدارة المستخدمين، الحجوزات، الدفع، السياسات، التكاملات، السجلات، والتسعير.

- Web (Customer): واجهة العملاء للحجز وإدارة الحساب والطلبات والمحفظة/النقاط (حسب تصميم المشروع).

- Admin: إدارة المحتوى والمنتجات والطلبات والعملاء والوكلاء والأدوار والمالية والتقارير.

- Mobile: تطبيق جوال (Offline-capable) يدعم وضع الضيف والمزامنة لاحقًا.

- Infra: DNS/SSL/WAF، الاستضافة، النشر، الأسرار، المراقبة، وحزم التسليم.

## 3.2 نموذج التفاعل مع مالك المشروع

يُعرَّف نموذج تشغيل الحسابات على أنه 'Owner-Assisted Authentication' أي أن المالك يقوم فقط بخطوات اعتماد الدخول/الدعوات/المصادقة الثنائية عند الحاجة، بينما تبقى عمليات الإعداد والربط والنشر والتهيئة مسؤولية فريق التنفيذ/المنصة.

# 4. الاستضافة والمزودون والمعايير الثابتة

وفقًا للمصدر المرجعي، تُعتمد المزودات التالية كاختيارات ثابتة للمشروع (ما لم يصدر قرار تغيير رسمي):

- --------------------------------------------------------

- Backend Hosting: Render (DO NOT USE Railway)

- Web + Admin: Vercel

- Database: Neon (PostgreSQL)

- DNS/SSL/WAF: Cloudflare

- Storage: Backblaze B2 (S3-compatible, signed URLs only)

- Push: Firebase FCM

- Domain/SMTP: Hostinger (as needed)

- novaxtravel.com

- www.novaxtravel.com

- api.novaxtravel.com

- admin.novaxtravel.com

- --------------------------------------------------------

## 4.1 النطاقات الفرعية المطلوبة

- novaxtravel.com

- www.novaxtravel.com

- api.novaxtravel.com

- admin.novaxtravel.com

# 5. الحوكمة والأمن وإدارة الأسرار

- مبدأ أقل صلاحية (Least Privilege) لكل مفاتيح/توكنات الوصول.

- تفضيل OAuth والدعوات الرسمية بدل كلمات المرور كلما أمكن.

- عدم تخزين الأسرار داخل الكود أو داخل ملفات ZIP؛ استخدام Secret Managers (GitHub/Render/Vercel) بحسب المزود.

- تفعيل SSL Full (Strict) على Cloudflare وربط DNS وإعداد قواعد WAF/Rate Limits الأساسية.

- تتبع السجلات (Audit Logs) للأحداث الحساسة (دخول، تغييرات صلاحيات، عمليات مالية).

# 6. البيئات (Staging و Production)

- Staging: بيئة اختبار واقعية على نفس الهيكلية لتجريب التحديثات قبل الإنتاج.

- Production: بيئة تشغيل المستخدمين النهائيين مع حماية وقيود صارمة وإجراءات Rollback.

- إدارة إعدادات كل بيئة عبر متغيرات بيئة منفصلة وملفات توثيق واضحة.

# 7. معايير القبول والتحقق (Definition of Done)

معايير القبول أدناه تُستخدم كمرجع تحقق للتسليم وليست تعليمات تنفيذ:

## 7.1 روابط تشغيل أساسية

- https://novaxtravel.com

- https://www.novaxtravel.com

- https://api.novaxtravel.com/health (must return OK)

- https://admin.novaxtravel.com (login works)

## 7.2 إثباتات الربط الخارجي

- Render service(s) created and running

- Vercel projects created and linked to domain

- Neon DB migrated + seeded

- Cloudflare DNS + Full (Strict) SSL + basic WAF/rate limits enabled

- Backblaze buckets integrated via signed URLs

- Firebase FCM configured

## 7.3 حزمة التسليم والتوثيق

- DEPLOYMENT.md (exact steps + architecture)

- ENV_VARIABLES_REFERENCE.md

- ROLLBACK.md

- ADMIN_OPERATIONS_GUIDE.md (non-technical)

- SECURITY.md

- API (OpenAPI/Swagger) + Postman collection (optional)

# 8. الفهرس المرجعي للفصول التفصيلية (كما وردت في المصدر)

القائمة التالية تمثل الفصول التفصيلية الموجودة في المصدر المرجعي، وتُستخدم كمرجع نطاق/تغطية:

- CHAPTER 2 – BRANDING & CORPORATE IDENTITY

- CHAPTER 3 – SYSTEM PHILOSOPHY & CORE

- CHAPTER 4 – AUTONOMOUS EXECUTION MANDATE FOR IMPLEMENTATION AGENT

- CHAPTER 5 – OWNER CONSTRAINTS & MANDATORY REQUIREMENTS

- CHAPTER 6 – FULL PLATFORM OVERVIEW

- CHAPTER 7 – BUSINESS DOMAIN CONTEXT

- CHAPTER 8 – YEMEN DOMAIN INTEGRATION

- CHAPTER 9 – SYSTEM ARCHITECTURE SUMMARY

- CHAPTER 10 – BACKEND ARCHITECTURE (LARAVEL API)

- CHAPTER 11 – CUSTOMER

- CHAPTER 12 – ADMIN CONTROL CENTER (NEXT.JS)

- CHAPTER 13 – MOBILE APPLICATION (FLUTTER ANDROID)

- CHAPTER 14 – OFFLINE SYSTEM & GUEST MODE

- CHAPTER 57 – DATA MATCHING BETWEEN AIRLINES, CITIES & GOVERNORATES

- CHAPTER 58 – FULL-TEXT SEARCH INDEXES FOR YEMEN DATA

- CHAPTER 59 – INTERNATIONAL EXPANSION DATA MODEL

- CHAPTER 60 – API

- CHAPTER 61 – YEMEN ROUTE NORMALIZATION & CLEANING ENGINE

- CHAPTER 62 – AIRPORT DISTANCE CALCULATION ENGINE

- CHAPTER 63 – SEASONAL PATTERN ENGINE FOR YEMEN ROUTES

- CHAPTER 71 – ADMIN-CONTROLLED GLOBAL

- CHAPTER 72 – ADMIN PANEL MASTER BUILDER (SCREEN-BY-SCREEN)

- CHAPTER 73 – SAFETY & RISK FACTOR ROUTING ENGINE (YEMEN-SPECIFIC)

- CHAPTER 74 – FUEL COST & DISTANCE MODEL (FUTURE-READY)

- CHAPTER 75 – TRAVEL DOCUMENTATION & COMPLIANCE RULES (YEMEN USERS)

- CHAPTER 76 – ADMIN-CONTROLLED GLOBAL BUILDER MODE

- CHAPTER 77 – UNIVERSAL IMPORT/EXPORT ENGINE

- CHAPTER 96 – ADMIN USER BEHAVIOR &

- CHAPTER 97 – ADMIN CRM ENGINE (CUSTOMER RELATIONSHIP MANAGEMENT)

- CHAPTER 98 – ADMIN COMMUNICATION CENTER (EMAIL/SMS/WHATSAPP CAMPAIGNS)

- CHAPTER 99 – ADMIN DATA MARKETPLACE (DATA EXPORT, APIs, SHARING TO PARTNERS)

- CHAPTER 100 – ADMIN BUSINESS INTELLIGENCE (BI) & VISUAL ANALYTICS BOARD

- CHAPTER 101 – SYSTEM ANTI-COLLAPSE FRAMEWORK (CORE PRINCIPLES)

- CHAPTER 102 – DATABASE

- CHAPTER 103 – SYSTEM FALLBACK & SAFE MODE ENGINE

- CHAPTER 104 – ZERO-DOWNTIME MIGRATION ENGINE

- CHAPTER 105 – RESOURCE LIMITER & SERVER PROTECTION

- CHAPTER 106 – STORAGE & FILE SYSTEM STABILITY ENGINE

- CHAPTER 107 – ADMIN PROTECTION FROM CRITICAL MISTAKES

- CHAPTER 108 – SELF-MONITORING & AUTO-HEALING ENGINE

- CHAPTER 109 – GLOBAL REDUNDANCY & MULTI-ZONE FAILOVER

- CHAPTER 110 – FINAL NON-NEGOTIABLE RULE: SYSTEM MUST NEVER COLLAPSE

- CHAPTER 111 – FULL DISASTER RECOVERY PLAYBOOK (AUTOMATED)

- CHAPTER 112 – SYSTEM GLOBAL CLONING ENGINE (REPLICATION ANYWHERE)

- CHAPTER 113 – DATA CORRUPTION DETECTION & AUTO-REPAIR

- CHAPTER 114 – RUNTIME INTEGRITY ENFORCEMENT ENGINE

- CHAPTER 115 – SYSTEM SELF-INTROSPECTION (AI MONITORING ITS OWN HEALTH)

- CHAPTER 116 – LOW-LEVEL KERNEL RATE LIMITING & OVERLOAD PROTECTION

- CHAPTER 117 – CONTINUOUS VALIDATION MONITOR (24/7 SYSTEM WATCHDOG)

- CHAPTER 118 – MULTI-REGION DATABASE SYNC ENGINE

- CHAPTER 119 – ADMIN PROJECT VALIDATION WIZARD (FINAL SYSTEM

- CHAPTER 120 – FINAL ANTI-COLLAPSE

- CHAPTER 121 – ADMIN AI GOVERNANCE & CONTROL FRAMEWORK

- CHAPTER 122 – SYSTEM SANDBOXING ENGINE (SAFE EXECUTION ENVIRONMENT)

- CHAPTER 123 – VIRTUALIZED RUNTIME ENVIRONMENT (PREVENTING SYSTEM DAMAGE)

- CHAPTER 124 – MULTI-HOST ORCHESTRATION ENGINE (SELF-MOVING SYSTEM)

- CHAPTER 125 – SERVICE MESH & MICROSERVICE ROUTER

- CHAPTER 126 – SCHEMA AUTO-EVOLUTION ENGINE (INTELLIGENT DB GROWTH)

- CHAPTER 127 – SYSTEM CLEANUP & OPTIMIZATION ENGINE

- CHAPTER 128 – RISK CLASSIFICATION SYSTEM (PREVENTING FAILURES)

- CHAPTER 129 – ADMIN SYSTEM LOCKDOWN MODE (MAXIMUM PROTECTION)

- CHAPTER 130 – FINAL STABILITY & UNBREAKABILITY GUARANTEES

- CHAPTER 131 – SYSTEM STRESS-TESTING & RESILIENCE ENGINE

- CHAPTER 132 – RUNTIME VIRTUALIZATION HYPERVISOR

- CHAPTER 133 – MULTI-CLOUD TRANSFER & PORTABILITY PROTOCOL

- CHAPTER 134 – REAL-TIME INTEGRITY LEDGER (BLOCKCHAIN-INSPIRED)

- CHAPTER 135 – PRICING & COMMISSION CORRECTNESS VALIDATOR

- CHAPTER 136 – LEGAL & REGULATORY COMPLIANCE FRAMEWORK

- CHAPTER 137 – CYBER-ATTACK IMMUNITY ARCHITECTURE

- CHAPTER 138 – GLOBAL RESILIENCE & REDUNDANCY GRID

- CHAPTER 139 – UNIVERSAL ADMIN EMERGENCY PANEL

- CHAPTER 140 – FINAL INSTRUCTIONS FOR IMPLEMENTATION AGENT

- CHAPTER 151 – ZERO-TRUST RUNTIME SECURITY POLICY

- CHAPTER 152 – GLOBAL API INSULATION & FALLBACK LAYER

- CHAPTER 153 – MULTIVERSE DEPLOYMENT ENVIRONMENTS

- CHAPTER 154 – UNIVERSAL SYSTEM ROLLBACK TECHNOLOGY

- CHAPTER 155 – COMPLIANCE-GRADE MONITORING & OBSERVABILITY SUITE

- CHAPTER 156 – ULTIMATE ADMIN CONTROL CORE (SUPER CONTROL ROOM)

- CHAPTER 157 – UNIVERSAL CONFIGURATION REGISTRY (EVERYTHING CENTRALIZED)

- CHAPTER 158 – QUANTUM STATE CHECKPOINTING (ADVANCED INTEGRITY)

- CHAPTER 159 – UNIVERSAL DATA NORMALIZATION ENGINE

- CHAPTER 160 – AUTONOMOUS SERVICE DEPENDENCY GRAPH (SDG)

- CHAPTER 170 – ADMIN-AS-DATABASE ENGINE

- CHAPTER 171 – ABSOLUTE SYSTEM NON-COLLAPSE GUARANTEE

- CHAPTER 172 – SCHEMA ARCHITECTURE REFERENCE

- CHAPTER 173 – MIGRATION MANAGEMENT ENGINE

- CHAPTER 174 – COST-LIMIT ENFORCEMENT & AUTO-OPTIMIZATION

- CHAPTER 176 – NOVAX UI/UX SYSTEM & CUSTOMER EXPERIENCE LAYER

- CHAPTER 177 – ADMIN-AS-DATABASE SYSTEM (FULL CRUD ENGINE & META-SCHEMA MANAGER)

- CHAPTER 203 – NOVAX_ASEM FINAL BUILD, PACKAGING & LIVE DEPLOYMENT ORDER

- CHAPTER 204 – ADVANCED SECURITY, OBSERVABILITY, CI/CD & BUSINESS CONTINUITY

- CHAPTER 209 – FINAL COMPLETION & MISSING SPEC PACKAGE

- CHAPTER 210 – DEPLOYMENT AUTHENTICATION & OWNER ACCESS POLICY

- CHAPTER 211 – POST-DEPLOYMENT GOVERNANCE, SECRET ROTATION & OWNER RUNBOOK

- CHAPTER 212 – LEGAL PAGES, CONSENT MANAGEMENT & POLICY VERSIONING

- CHAPTER 213 – PAYMENT, FINANCIAL COMPLIANCE & AUDIT-READY LEDGER

- CHAPTER 214 – RELEASE MANAGEMENT, APK SIGNING & APP DISTRIBUTION POLICY

- CHAPTER 215 – ANALYTICS, PRODUCT METRICS & CONSENT-RESPECTING TELEMETRY

- CHAPTER 218 – ACCESSIBILITY, UX BASELINE & RTL-READINESS

- CHAPTER 219 – SEO, INDEXING, PUBLIC PAGES & CONTENT POLICY

- CHAPTER 220 – PERFORMANCE BUDGET, LOAD TARGETS & CACHING POLICY

- CHAPTER 221 – SUPPORT OPERATIONS, TICKETING & CUSTOMER SERVICE SLA

- CHAPTER 222 – DATA QUALITY, MASTER DATA GOVERNANCE & APPROVAL WORKFLOWS

- CHAPTER 223 – SENSITIVE DATA ACCESS COMPLIANCE, MASKING & ABNORMAL-ACCESS ALERTS

- CHAPTER 224 – BUSINESS CONTINUITY, SAFE MODE & OFFLINE OPERATIONS PLAYBOOK

- CHAPTER 225 – THIRD-PARTY INTEGRATIONS GOVERNANCE, SAFE CONNECTORS & KILL SWITCH

- CHAPTER 226 – FINAL GO-LIVE CHECKLIST, EVIDENCE PACKAGE & OWNER SIGN-OFF

- CHAPTER 227 – RELIABILITY, SELF-HEALING & OPERATIONS HARDENING ADDENDUM


# الملحق A: النص المرجعي الأصلي بصياغة وصفية (English Reference)

ملاحظة: هذا الملحق يُدرج النص المرجعي الأصلي بعد تخفيف صياغة الأوامر المباشرة، للاحتفاظ بكل التفاصيل.

READ FIRST — OWNER-AUTHORIZED LOGIN / FULL AUTONOMOUS BUILD & DEPLOY

NOVAX TRAVEL — EXTERNAL PRODUCTION ONLY (NO PROVIDER-OWNED HOSTING)

You are the Implementation Agent (AI system or engineering team), engaged as the senior full-stack implementation team (architecture + DevOps + security + backend + web + admin + mobile).

Project objective is to BUILD, DEPLOY, SECURE, and DELIVER NOVAX TRAVEL as a LIVE PRODUCTION SYSTEM (not a prototype, not documentation-only).

0) SOURCE OF TRUTH

This document is the ONLY source of truth.

Read it completely first, then execute end-to-end.

If anything is unclear, apply best practices and continue without blocking.

1) OWNER-ASSISTED AUTHENTICATION MODE (THIS IS HOW YOU ACCESS ACCOUNTS)

The Owner will NOT deploy manually.

The Owner will ONLY do:

- Login to his own provider accounts on his device

- Approve OAuth prompts

- Approve MFA/2FA prompts

- Accept invitations

- (If unavoidable) paste ONE-TIME tokens/keys that you request, once

The delivery must do everything else: setup, wiring, CI/CD, migrations, seeding, deployment, domain linking, SSL/WAF, monitoring, and final verification.

SECURITY RULE:

- Prefer OAuth + invitations over passwords.

- DO NOT ask for master passwords if invite/OAuth is possible.

- Use least-privilege tokens only when required.

- Never store secrets in code or in the ZIP; use provider secret managers (Render/Vercel/GitHub Secrets).

2) HARD RULE: EXTERNAL DEPLOYMENT ONLY (NO PROVIDER-OWNED HOSTING)

Production MUST be deployed on the Owner’s external accounts and domain.

Forbidden: hosting production inside the provider hosting or the provider-owned infrastructure.

the provider internal environment may be used ONLY for temporary build/test.

3) FIXED PROVIDERS (DO NOT CHANGE)

- Backend Hosting: Render (DO NOT USE Railway)

- Web + Admin: Vercel

- Database: Neon (PostgreSQL)

- DNS/SSL/WAF: Cloudflare

- Storage: Backblaze B2 (S3-compatible, signed URLs only)

- Push: Firebase FCM

- Domain/SMTP: Hostinger (as needed)

Domain:

- novaxtravel.com

Required subdomains:

- www.novaxtravel.com

- api.novaxtravel.com

- admin.novaxtravel.com

4) ONE-TIME ACCESS PACKET (ASK ONCE ONLY, ONE MESSAGE)

Before implementation, ask for access in ONE consolidated message only.

Request ONLY:

1) GitHub: invite collaborator/team OR OAuth connect

2) Render: team invite OR scoped token + connect to GitHub

3) Vercel: OAuth approval + connect to GitHub

4) Neon: invite OR restricted DB connection string

5) Cloudflare: scoped token (DNS edit + SSL/TLS + WAF/rate rules)

6) Backblaze: app key limited to required buckets

7) Firebase: invite OR service account for FCM only

8) Hostinger: SMTP creds only if needed

After owner completes authentication, proceed without further questions.

5) DEFINITION OF DONE (The delivery must DELIVER THIS OR IT IS REJECTED)

A) Live URLs working:

- https://novaxtravel.com

- https://www.novaxtravel.com

- https://api.novaxtravel.com/health (must return OK)

- https://admin.novaxtravel.com (login works)

B) Proof of external deployment (owner accounts):

- Render service(s) created and running

- Vercel projects created and linked to domain

- Neon DB migrated + seeded

- Cloudflare DNS + Full (Strict) SSL + basic WAF/rate limits enabled

- Backblaze buckets integrated via signed URLs

- Firebase FCM configured

C) Handover package inside final ZIP:

- DEPLOYMENT.md (exact steps + architecture)

- ENV_VARIABLES_REFERENCE.md

- ROLLBACK.md

- ADMIN_OPERATIONS_GUIDE.md (non-technical)

- SECURITY.md

- API (OpenAPI/Swagger) + Postman collection (optional)

D) Final statement required:

“Production is deployed only on the Owner’s accounts. No the provider hosting is used.”

END OF READ FIRST

# **CHAPTER 1 – EXECUTIVE SUMMARY**

## *(Full English Version for the Implementation Agent – NOVAX TRAVEL Master Execution Document)*

NOVAX TRAVEL is a fully integrated, production-grade travel management ecosystem designed for the Yemeni market and for global scalability. This Master Request Document serves as the **complete and authoritative execution mandate** instructing **the Implementation Agent** to autonomously design, build, deploy, secure, configure, and deliver the entire platform **without requesting any technical clarification** from the owner.

The system must support:

* Domestic Yemeni flights (manual, non-API)

* Global flights (future API integrations)

* Hotel booking

* Car & ground transport

* Visa processing

* Offline mobile operation

* Guest mode (full usability without registration)

* Payment through uploaded bank receipts (Al-Kuraimi)

* Multi-role, multi-agency, and multi-company structure

* Full RBAC with granular permission controls

* Dynamic pricing engine

* Request lifecycle engines (state machines)

* Cloud infrastructure automation

* Unified admin control center

* Full audit trails & security logging

* Enterprise-grade monitoring and incident response

* CI/CD pipelines for automated deployment

* Branding, theming, and identity management

* API-driven, modular architecture

* Zero-trust security posture across all layers

The purpose of this document is to instruct the Implementation Agent to autonomously generate:

* Backend (Laravel API)

* Web platform (Next.js Customer Portal)

* Admin dashboard (Next.js Control Center)

* Mobile application (Flutter Android, offline-first)

* PostgreSQL database (Neon)

* Object storage (Backblaze B2)

* DNS, SSL, WAF (Cloudflare)

* CI/CD pipelines (GitHub Actions)

* Analytics dashboards & BI

* Security frameworks, IDS, audit logs

* OTA update system for mobile

* All workflows, automations, and operational logic

NOVAX TRAVEL must be built as a **complete, immediately deployable production system**, running on low-cost infrastructure (≈$300/year), with no manual coding, database access, or command-line intervention required by the owner.

the Implementation Agent must follow:

* **Autonomous Execution**: all technical decisions are made by the Implementation Agent.

* **Best-Practice Defaults**: whenever unclear, the Implementation Agent uses industry standards.

* **Full Delivery**: the output must be a functioning, fully documented platform.

* **No Timelines**: the document contains zero schedules or time estimates.

The final system must be:

* **Robust** – able to handle large user volumes and agents

* **Secure** – built with zero-trust, MFA, encryption, IDS, and audit logs

* **Scalable** – horizontally expandable at all layers

* **Portable** – not locked into any single provider

* **Maintainable** – fully controllable from the Admin Panel

* **Offline-Capable** – especially the mobile application

* **Localized** – with full Yemeni domain data pre-seeded

This document is not an outline.

It is a **full technical charter**, containing:

* All architecture

* All workflows

* All state machines

* All pricing logic

* All admin functionality

* All security controls

* All datasets (Yemen routes, cities, governorates, airlines, etc.)

* All infrastructure definitions

* All user journeys

Once this providercript is complete and merged into a single text block, the Implementation Agent will use it as the **sole reference** to construct NOVAX TRAVEL from end to end.

CHAPTER 2 – BRANDING & CORPORATE IDENTITY

NOVAX TRAVEL must be delivered with a fully defined global-quality brand identity. the Implementation Agent is responsible for generating all brand assets, applying them consistently, and integrating them across Web, Admin, and Mobile experiences.

2.1 Brand Personality

NOVAX TRAVEL’s identity must reflect:

Professionalism

Modernity

Trust and reliability

Technical sophistication

Simplicity and clarity

Speed and intelligence

Global ambition

Stability and security

2.2 Color Palette (Mandatory Across All Interfaces)

Primary Colors:

NOVAX Blue: #1D4ED8

NOVAX Teal: #0EA5E9

Secondary Colors:

Deep Navy: #0F172A

White: #FFFFFF

Gray Scale: #F8FAFC → #1E293B

2.3 Typography System

Primary Font: Inter

Secondary Font: Roboto

Monospace Font: JetBrains Mono (for code blocks, diagrams, system outputs)

2.4 Branding Assets Required

the Implementation Agent must generate:

Logo pack (Light/Dark) – SVG, PNG

Favicon set

Mobile app icons (Android)

Splash screens (Mobile)

Email logos

PDF ticket headers & footers

Visual identity guideline document (Brand Book)

2.5 UI/UX Design Principles

Minimalist and clean

Strong contrast

Accessible

Performance-focused

Consistent across all platforms

Adaptive for RTL (Arabic) and LTR (English)

Responsive for all screen sizes

CHAPTER 3 – SYSTEM PHILOSOPHY & CORE

PRINCIPLES

NOVAX TRAVEL is built on foundational technical and operational principles that guide all systems, workflows, and architectural decisions.

3.1 Autonomy

the Implementation Agent must execute all technical decisions independently.

The owner is not a programmer and will not determine architectural choices.

3.2 Zero-Trust Security Model

Every component, API request, and user session must be treated as untrusted by default.

3.3 Portability

The system must avoid vendor lock-in.

All components must be transferable to equivalent providers (AWS, DO, GCP, etc.).

3.4 Offline-First Mobile

Architecture

The mobile app must function:

Without network

With intermittent network

With slow or unstable connectivity

Using:

Local database (SQLite/Hive)

Local caching

Background sync engine

Delta updates

3.5 Admin-Operated System

Daily operations must be possible entirely through the Admin Panel:

Configuration

Pricing

Agents

Corporate accounts

Content

Workflows

Policies

No SQL.

No code editing.

No terminal access.

3.6 Scalability

System must support:

Millions of users

Thousands of agents

Large datasets

Horizontal scaling

3.7 Observability

System must include:

Full audit logs

Error tracking

Security alerts

Health monitoring

Analytics dashboards

3.8 Localization & Yemen Focus

Yemen domain data is mandatory:

Governorates

Cities

Airlines

Routes

Domestic flight logic

3.9 User Empowerment

User journeys must be frictionless:

Guest mode

Simple booking

Clear UX

Low-bandwidth compatibility

CHAPTER 4 – AUTONOMOUS EXECUTION MANDATE FOR IMPLEMENTATION AGENT

This chapter defines the non-negotiable authority and responsibilities of the Implementation Agent.

4.1 Full Technical Autonomy

the Implementation Agent must:

Determine all frameworks and patterns

Select all libraries

Establish infrastructure

Create repositories

Configure environments

Deploy all services

Set up CI/CD

Create admin accounts

Seed initial data

Secure the entire system

Document all processes

4.2 Non-Negotiable Restrictions on the Implementation Agent

the Implementation Agent must not:

Ask technical questions

Ask for architectural decisions

Request schema design input

Request UI design guidance

Request workflow clarification

If any detail is unclear:

Apply best-practice industry standards and

proceed.

4.3 Responsibilities Across the Entire Stack

the Implementation Agent must deliver:

Backend API (Laravel)

Customer Web Portal (Next.js)

Admin Control Center (Next.js)

Android Application (Flutter)

Mobile Sync Engine

OTA System

Storage (Backblaze B2)

Database (Neon PostgreSQL)

DNS/SSL/WAF (Cloudflare)

Notifications (Email, Push)

Analytics & BI

Security Systems

Log Processing

Incident Response workflows

Documentation, runbooks, and admin guides

CHAPTER 5 – OWNER CONSTRAINTS & MANDATORY REQUIREMENTS

These constraints must be respected everywhere in the system:

5.1 Budget Constraint

~300 USD per year total infrastructure cost.

5.2 Operational Constraints

Owner will not write code

Owner will not use SQL

Owner will not configure servers

All daily operations must be visual (Admin Panel)

5.3 Market Constraints

Yemen is the primary operational domain

Offline operation required

Domestic flight system must be manual (non-API)

Payment primarily via bank transfer receipts

Support extremely low bandwidth environments

5.4 Technology Constraints

Web stack: Next.js

Backend: Laravel

Mobile: Flutter Android

DB: PostgreSQL

Storage: Backblaze

Delivery: OTA updates

CHAPTER 6 – FULL PLATFORM OVERVIEW

NOVAX TRAVEL is composed of multiple interconnected systems forming a unified ecosystem.

6.1 Customer-Facing Services

Flight search

Hotel search & bookings

Ground transport (cars)

Visa request system

Wallet

Loyalty points

Notifications

User profile

Guest mode (fully operational)

6.2 Internal Business Systems

Admin control center

CRM-like agent management

Corporate account hierarchies

Pricing engine

Commission engine

Request lifecycle engines

Full auditing system

Notifications hub

Analytics and BI dashboards

6.3 Integrations

TravelPayouts / Duffel (future)

Cloudflare (DNS, SSL, WAF)

Backblaze B2 (object storage)

Firebase FCM (push notifications)

SMTP mail provider

Al-Kuraimi receipts (manual verification)

CHAPTER 7 – BUSINESS DOMAIN CONTEXT

NOVAX TRAVEL operates in a unique business and technical environment, especially within Yemen.

7.1 Market Challenges

No official airline APIs

Manual booking workflows

High dependency on agents

Frequent internet outages

Slow or unstable connectivity

Banks require manual transfers

Local travel patterns are irregular

Pricing varies dynamically

7.2 Operational Use Cases

Domestic flight booking

International flight lookup

Hotel reservation

Visa processing

Inter-city transport

Corporate travel management

Agent-driven bookings

7.3 User Types

Individual customers

Guest users

Companies

Corporate employees

Travel agents

Sub-agents

Administrators

Finance team

Support team

CHAPTER 8 – YEMEN DOMAIN INTEGRATION

NOVAX TRAVEL must include a complete, pre-seeded dataset representing the Yemen travel ecosystem, enabling domestic operations even without internet connectivity or API integrations.

8.1 Governorates (22 Total)

Each governorate must include:

id

name_ar

name_en

capital_ar

capital_en

region_code

latitude

longitude

status

List of All Governorates

Amanat Al-Asimah (Sana’a City)

Sana’a

Aden

Taiz

Lahj

Abyan

Shabwah

Hadhramaut

Al Mahrah

Marib

Al Jawf

Sa’dah

Amran

Dhamar

Ibb

Raymah

Al Bayda

Al Hudaydah

Al Mahwit

Hajjah

Al Dhale’e

Socotra

8.2 Cities

Each city must include:

id

governorate_id

name_ar

name_en

city_type (capital, airport_city, major_city, tourist_city, regular)

latitude

longitude

status

Mandatory Airport Cities

Aden

Seiyun

Riyan/Mukalla

Ghaidah

Socotra

Sana’a (inactive but must be included)

Taiz

Al-Hudaydah

8.3 Yemeni Airlines

Required:

Yemenia (IY)

Felix Airways / Al Saeeda (FDY)

Queen Bilqis Airways

Aden Airways

Private charter operators

Fields:

id

code

name_ar

name_en

iata_code

icao_code

baggage_policy

logo_url

status

8.4 Domestic Flight Routes

Each route must include:

origin_city_id

destination_city_id

airline_id

weekday_pattern

seasonal flags

duration

base_price

price_range

status

Core Domestic & Regional Routes

From Seiyun:

Seiyun → Jeddah

Seiyun → Cairo

Seiyun → Khartoum

Seiyun → Amman

From Aden:

Aden → Jeddah

Aden → Riyadh

Aden → Cairo

Aden → Doha

From Riyan (Mukalla):

Riyan → Jeddah

Riyan → Sharjah

Riyan → Cairo

From Ghaidah:

Ghaidah → Jeddah

Ghaidah → Amman

8.5 Ground Transport Operators

A complete dataset for:

Inter-city transport

Private drivers

Car rental services

Fields:

id

name

governorate_id

car_type

capacity

base_price

pricing_model

phone

status

CHAPTER 9 – SYSTEM ARCHITECTURE SUMMARY

NOVAX TRAVEL is a multi-tier, distributed system composed of:

Frontend Web

Mobile App (Offline-first)

Backend API

Database

Storage

CDN/WAF

CI/CD pipelines

Background workers

Sync engine

9.1 High-Level ASCII

Architecture Diagram

[ Users / Agents / Companies ] | v [ Next.js Web Portal ] | v [ Laravel Backend API Layer ] | ------------------------------------------------- | | [ PostgreSQL (Neon) ] [ Backblaze B2 ] | | v v [ Background Jobs ] [ Static Assets ] | v [ Sync Engine / Notifications ] | v [ Flutter Mobile App (Offline Mode) ] | v [ Cloudflare DNS + SSL + WAF ]

CHAPTER 10 – BACKEND ARCHITECTURE (LARAVEL API)

The backend API is the operational core of NOVAX TRAVEL.

10.1 Required Features

Laravel 10+

JWT authentication

Role-based middleware

Eloquent ORM

Repository + Service Layer pattern

Global exception handler

Request validation

Resource transformers

Versioned API endpoints

Full logging & monitoring

10.2 Core API Modules

Authentication & MFA

Users

Roles & Permissions (RBAC)

Agencies

Companies

Flights (Manual Yemeni Flights)

Hotels

Cars & Transport

Visas

Pricing Engine

Commissions Engine

Requests Engine (State Machine)

Notifications

Wallet & Loyalty

Files (Backblaze Integration)

System Settings

Yemen Domain Module

10.3 Security Requirements

Rate limiting per IP

MFA enforcement

Password hashing (bcrypt)

AES-256 encryption for sensitive fields

Signed URLs for private files

Brute-force protection

Action logging

10.4 Background Jobs

Payment verification

Syncing offline requests

Pushing notifications

Clearing old sessions

Price recalculations

CHAPTER 11 – CUSTOMER

WEB PORTAL (NEXT.JS)

The customer web portal provides full access to all public-facing services.

11.1 Key Functionalities

Search flights (domestic & global future)

View flight details

Create booking requests

Upload bank receipt

Track requests

Manage profile

Access loyalty and wallet

Submit hotel/car/visa requests

Operate fully as Guest user

11.2 Technical Stack

Next.js 14+

TypeScript

TailwindCSS

Server Actions

Client caching (SWR/React Query)

i18n for Arabic & English

Responsive design

11.3 Security

HTTPS enforced

Client-side sanitization

Input validations

Cloudflare WAF

Captcha for repeated failures

CHAPTER 12 – ADMIN CONTROL CENTER (NEXT.JS)

The Admin Panel is the operational center of the entire ecosystem.

12.1 Modules

1. Dashboard

KPIs

Activity logs

Request statistics

Agent performance

2. Users Management

Create/edit users

Roles assignment

MFA enforcement

3. Roles & Permissions (RBAC)

Create/Edit roles

Assign granular permissions

Sensitive operations require MFA

4. Agencies

Commission rules

Balance

Performance reports

5. Corporate Accounts

Employees

Custom pricing rules

Spending limits

6. Domestic Yemeni Flights

Add/upload schedules

Set availability

Modify prices

Monitor seats

7. Pricing Engine

Create pricing rules

Tiered rules

Bundles

Seasonal pricing

Agent/customer group pricing

8. Requests Engine

View all requests

Move between states

Upload tickets/visas

Reject/approve requests

9. Notifications Center

Email templates

Push notification templates

10. Audit Log Viewer

Full transparency of system actions

11. System Settings

Branding

Maintenance mode

Feature flags

API keys

12. BI Dashboards

Financial charts

Operations charts

Agent analytics

CHAPTER 13 – MOBILE APPLICATION (FLUTTER ANDROID)

13.1 Requirements

Fully offline-capable

Local storage (SQLite/Hive)

Background synchronization

Push notifications via FCM

OTA updates

Optimized for low-bandwidth usage

13.2 Functionalities

Search and book flights

Track all requests

Upload receipts

Guest mode

Profile management

Offline caching

CHAPTER 14 – OFFLINE SYSTEM & GUEST MODE

14.1 Offline Capabilities

Mobile app must store:

Yemen domain dataset

Saved searches

Cached results

Pending requests

User session data

14.2 Guest Mode

Guest users can:

Search flights

Submit booking requests

Upload payment receipts

Receive SMS/email updates

Later convert to full account

Continuing with **multiple full chapters in each message** until the complete English providercript is finished.

# **CHAPTER 15 – AUTHENTICATION, MFA & SECURITY FRAMEWORK**

Security is a first-class requirement of NOVAX TRAVEL.

All authentication, identity, session management, and MFA systems must follow modern zero-trust principles.

## **15.1 Authentication Model**

* JWT Access Tokens

* Refresh Tokens

* Device Fingerprinting

* Session TTL

* Forced Logout on critical changes

* Password hashing (bcrypt)

* Email/phone login support

## **15.2 Account Registration**

Mandatory fields:

* Full name

* Phone number

* Email address

* Password

* Country of residence (optional)

Verification:

* OTP via email (default)

* OTP via SMS (future-ready)

## **15.3 Login Process**

Flow:

1. User enters email/phone + password

2. System validates credentials

3. System checks risk level

4. If risk detected → MFA enforced

5. JWT access/refresh tokens returned

## **15.4 Multi-Factor Authentication (MFA)**

Types supported:

* Email OTP

* Authenticator app (TOTP)

* SMS OTP (future option)

MFA Modes:

* **Optional**

* **Required** for sensitive roles (Finance, Admin, Super Admin)

* **Forced** on suspicious logins

## **15.5 Zero-Trust Security Rules**

* Every API request is authenticated

* Every privileged action is re-authorized

* Tokens rotate frequently

* Session revocation triggers immediate logout

## **15.6 Sensitive Operations Require MFA**

Actions requiring MFA:

* Pricing rule changes

* Role/permission updates

* Financial adjustments

* Agency commission changes

* Ticket/visa issuance approval

## **15.7 Encryption Requirements**

* AES-256 for sensitive fields (ID numbers, passport data, uploaded documents)

* Signed URLs for file downloads

* Encrypted local storage on mobile

## **15.8 Rate Limiting**

* Per user

* Per IP

* Per endpoint type

* Adaptive throttling on suspicious activity

# **CHAPTER 16 – RBAC, ROLES, PERMISSIONS & ENTERPRISE HIERARCHY**

NOVAX TRAVEL must implement a **granular enterprise-grade RBAC system**, supporting:

* User roles

* Permission groups

* Multi-level agencies

* Corporate accounts

* Sub-users

* Delegated access

## **16.1 Role Hierarchy**

Mandatory system roles:

1. **Super Admin**

2. **Admin**

3. **Finance Manager**

4. **Travel Supervisor**

5. **Ticketing Officer**

6. **Visa Officer**

7. **Car/Transport Operator**

8. **Hotel Operator**

9. **Support Specialist**

10. **Agent Owner**

11. **Sub-Agent**

12. **Corporate Admin**

13. **Corporate Employee**

14. **Customer**

## **16.2 Permission System**

Each permission must be individually

assignable, including:

* View / Create / Update / Delete

* Approve / Reject

* Financial actions

* Sensitive operations (require MFA)

* Reporting permissions

* System configuration access

* Flight pricing management

* Visa processing management

## **16.3 Agencies Module**

Agents must have:

* Balance

* Commission rates

* Assigned sub-agents

* Custom pricing policies

* Sales performance reports

* Booking rights

* Invoice histories

## **16.4 Corporate Accounts**

Corporations receive:

* Custom pricing

* Employee accounts

* Spending limits

* Monthly invoicing

* Approval workflows

## **16.5 Delegated Access**

Corporate Admins can:

* Add employees

* Remove employees

* Limit spending per employee

* Restrict allowed services

* Review employee bookings

# **CHAPTER 17 – DATABASE ARCHITECTURE (150+ TABLES)**

NOVAX TRAVEL requires a normalized, indexed, relational schema with JSONB support.

## **17.1 DB Requirements**

* PostgreSQL (Neon)

* Normalized schema

* Referential integrity

* Indexes on major fields

* Soft deletes where appropriate

* Background migrations

* Staging + Production branches

* PITR support

## **17.2 Core Tables**

Below is a partial but mandatory list:

### **Users & Identity**

* users

* roles

* permissions

* role_permission_map

* user_role_map

* mfa_configs

* devices

### **Travel Data**

* flights_manual

* flight_schedules

* flight_fares

* flight_segments

* airlines

* yemen_governorates

* yemen_cities

* yemen_routes

### **Requests**

* requests

* request_states

* request_documents

* request_messages

### **Hotels**

* hotels

* hotel_rooms

* hotel_prices

* hotel_requests

### **Cars & Transport**

* car_drivers

* car_routes

* car_requests

### **Visas**

* visa_countries

* visa_requirements

* visa_requests

### **Financial**

* wallet_transactions

* loyalty_points

* pricing_rules

* commission_rules

* invoices

* receipts

### **Logging & Security**

* audit_logs

* security_events

* login_attempts

* system_settings

# **CHAPTER 18 – PRICING ENGINE**

The Pricing Engine is one of the most critical components of NOVAX TRAVEL.

## **18.1 Pricing Rule Types**

1. **Percentage Markup**

2. **Fixed Amount Markup**

3. **Tiered Pricing (Based on ranges)**

4. **Conditional Pricing (based on user,

service, location, season)**

5. **Bundles (Flight + Car, Flight + Hotel, etc.)**

6. **Agent-specific overrides**

7. **Corporate pricing contracts**

## **18.2 Example Pricing Rules**

* +10% on all Yemenia flights

* +$20 fixed markup for all car bookings

* +5% if booking within 24 hours of departure

* Special corporate discount of 12%

* If service bundle = (Hotel + Car) → apply 8% discount

## **18.3 Pricing Application Flow**

```

Base Fare

↓

Apply Global Rules

↓

Apply Service-Specific Rules

↓

Apply Agent/Corporate Overrides

↓

Apply Bundles

↓

Final Price

```

## **18.4 Pricing Engine Features**

* Rule priority

* Rule activation/deactivation

* Rule simulation tool in Admin Panel

* Real-time recalculation

* Logging of which rules were applied

# **CHAPTER 19 – PAYMENTS, WALLET & LOYALTY SYSTEM**

## **19.1 Payment Method**

Primary payment method:

* **Bank receipt upload (Al-Kuraimi)**

* Upload image

* Enter transaction reference

* Finance manually verifies

* Status transitions:

* Pending

* Verified

* Rejected

Future payment gateways must be

integratable.

## **19.2 Wallet System**

Wallet features:

* Add credit

* Deduct credit

* Auto-deduct on bookings

* Agent balances

* Corporate balances

* Transaction histories

wallet_transactions fields:

* id

* user_id

* type (credit/debit)

* amount

* reference

* service_type

* created_at

## **19.3 Loyalty Points**

Rules:

* 1 USD spent = 1 point

* 500 points = $1 redeemable

* Points added after request completion

* Points shown in user dashboard

# **CHAPTER 20 – REQUEST LIFECYCLE ENGINE**

All services must follow a unified state machine.

## **20.1 States**

1. Pending

2. In Review

3. Awaiting Payment

4. Payment Verification

5. In Progress

6. Approved

7. Ticketed / Issued

8. Completed

9. Cancelled

10. Rejected

## **20.2 ASCII State Machine Diagram**

```

[PENDING]

|

v

[IN REVIEW] --> [REJECTED]

|

v

[AWAITING PAYMENT]

|

v

[PAYMENT VERIFICATION] --> [REJECTED]

|

v

[IN PROGRESS]

|

v

[APPROVED]

|

v

[TICKETED / ISSUED]

|

v

[COMPLETED]

```

## **20.3 System Responsibilities**

At each state:

* Notifications must be triggered

* Logs must be recorded

* Permissions checked

* SLA timers started/stopped

* Auto-escalation if delays occur

Continuing with **multiple full chapters per message**, fully detailed, until the entire English providercript is completed.

# **CHAPTER 21 – YEMEN DOMAIN DATASET (DETAILED STRUCTURE)**

This dataset is mandatory for NOVAX TRAVEL’s offline search, manual flight operations, and domestic travel workflows.

the Implementation Agent must fully seed all of these datasets during system initialization.

## **21.1 Governorates Table Structure**

Required fields:

* id (INT)

* name_ar (TEXT)

* name_en (TEXT)

* capital_ar (TEXT)

* capital_en (TEXT)

* region_code (TEXT)

* latitude (FLOAT)

* longitude (FLOAT)

* status (BOOLEAN)

## **21.2 Cities Table Structure**

Fields:

* id

* governorate_id

* name_ar

* name_en

* city_type (airport_city / major_city / capital / tourist / regular)

* latitude

* longitude

* status

### **Cities with Airports (Mandatory):**

* Sana’a

* Aden

* Seiyun

* Riyan (Mukalla)

* Ghaidah

* Al-Hudaydah

* Taiz

* Socotra

## **21.3 Airline Table Structure**

Fields:

* id

* name_ar

* name_en

* code

* iata_code

* icao_code

* logo_url

* baggage_policy (JSON)

* status

### **Required Yemeni Airlines:**

1. Yemenia

2. Felix Airways (Al Saeeda)

3. Queen Bilqis Airways

4. Aden Airways

5. Charter operators

## **21.4 Flight Routes Table Structure**

Fields:

* id

* origin_city_id

* destination_city_id

* airline_id

* weekday_pattern (JSON: [Mon, Tue, Wed…])

* seasonality_flags

* flight_duration

* base_price

* price_range_min

* price_range_max

* status

## **21.5 Ground Transport Dataset**

Fields:

* id

* operator_name

* governorate_id

* car_type

* capacity

* base_price

* per_km_price

* phone_number

* status

## **21.6 Hotels Dataset**

Fields:

* id

* name_ar

* name_en

* city_id

* stars

* price_min

* price_max

* amenities (JSON)

* images

* status

## **21.7 Visa Destinations Table**

Fields:

* id

* country_name

* processing_time_days

* required_documents (JSON)

* base_price

* notes

* status

# **CHAPTER 22 – TRIP SEARCH ENGINE**

The Trip Search Engine provides unified search across:

* Domestic Yemeni flights (manual)

* International flights (future API integration)

## **22.1 Search Input Parameters**

* origin

* destination

* date_of_travel

* passengers_count

* cabin_type (optional)

* user_type (guest/customer/agent/corporate)

## **22.2 Search Processing Logic**

1. Validate route

2. Load cached domestic schedules

3. Apply pricing rules

4. Fetch future API provider data (if enabled)

5. Merge domestic & international results

6. Sort by:

* lowest price

* shortest duration

* earliest departure

## **22.3 Unified Search Output Structure**

```

[

{

"airline": "...",

"origin": "...",

"destination": "...",

"departure_time": "...",

"arrival_time": "...",

"duration": "...",

"base_price": "...",

"final_price": "...",

"baggage": "...",

"seats_available": "...",

"source": "domestic/manual or

global_api",

}

]

```

## **22.4 Offline Search Mode**

When offline:

* Use last synchronized Yemen dataset

* Show cached results

* Allow request submission (queued for sync)

# **CHAPTER 23 – MANUAL YEMENI

FLIGHT BOOKING ENGINE**

Since Yemeni airlines do not have APIs, NOVAX TRAVEL must implement a full **manual flight management system**.

## **23.1 Booking Steps**

1. User selects a flight

2. Enters passenger details

3. Uploads documents (passport, ID)

4. Sends booking request

5. Request enters **Pending** state

6. Travel officer reviews

7. Pricing engine recalculates final fare

8. Finance verifies payment receipt

9. Travel team issues ticket

10. Ticket uploaded to request

11. User notified

12. Request marked **Ticketed** → **Completed**

## **23.2 Required Passenger Fields**

* Full name (English as per passport)

* Date of birth

* Nationality

* Passport number

* Passport expiry date

* Gender

* Phone number

## **23.3 Ticket Upload Requirements**

Format supported:

* PDF

* Image (PNG/JPG)

* Secure download via signed URL

# **CHAPTER 24 – CAR & GROUND TRANSPORT SYSTEM**

This system enables inter-city and local travel booking.

## **24.1 User Journey**

1. Select origin city

2. Select destination

3. Choose car type

4. View pricing

5. Submit request

6. Operator assigns driver

7. User receives updates

8. Trip completed → user rated (future feature)

## **24.2 Driver Table Structure**

* id

* name

* governorate_id

* car_type

* capacity

* base_price

* per_km_price

* phone

* status

## **24.3 Car Type Examples**

* Sedan

* SUV

* Minivan

* Bus

* VIP car

# **CHAPTER 25 – HOTEL BOOKING SYSTEM**

NOVAX TRAVEL must support hotel search, internal inventory, and manual processing of bookings.

## **25.1 Search Filters**

* City

* Price range

* Star rating

* Amenities

* Room type

## **25.2 Hotel Page Must Display**

* Photos

* Description

* Room availability

* Price range

* Amenities list

* Terms and policies

## **25.3 Hotel Request Workflow**

1. User selects room

2. Enters guest details

3. Uploads optional documents

4. Request created

5. Operator reviews availability

6. Confirms booking

7. Uploads invoice/ticket

8. Request moves to **Completed**

# **CHAPTER 26 – VISA PROCESSING SYSTEM**

A full visa management system must be included.

## **26.1 Supported Countries (Expandable)**

* Saudi Arabia

* Egypt

* Jordan

* UAE

* Turkey

* India

* Malaysia

## **26.2 Visa Request Steps**

1. User selects a destination country

2. Views required documents

3. Uploads passport + documents

4. Operator reviews

5. Request processed with external visa service

6. Visa issued

7. PDF uploaded

8. User notified

# **CHAPTER 27 – NOTIFICATIONS

ENGINE**

Notifications are a critical cross-system feature.

## **27.1 Channels**

* Email

* Push notifications (mobile)

* In-app messages

* SMS (future integration)

## **27.2 Triggers**

* New request

* State change

* Payment verification

* Ticket issuance

* Rejection

* Missing documents alerts

* SLA breach alerts

## **27.3 Notification Template Engine**

Admin must configure:

* Subject

* Message body

* Dynamic placeholders

* Multi-language templates

# **CHAPTER 28 – AUDIT LOGS, SECURITY EVENTS & IDS**

This is the core of compliance and risk detection.

## **28.1 Mandatory Logged Actions**

* Login / logout

* Failed login attempts

* Role/permission changes

* Pricing rule updates

* Request approvals

* Payment verifications

* Ticket issuance

* File uploads

* System settings changes

## **28.2 Audit Log Table Structure**

* id

* user_id

* action

* entity_type

* entity_id

* old_value

* new_value

* ip_address

* user_agent

* created_at

## **28.3 Intrusion Detection System (IDS)**

Detects:

* Brute-force login attempts

* Suspicious API access

* Elevated privilege abuse

* Abnormal request volumes

* Document upload anomalies

* Server errors indicating attacks

## **28.4 Automatic Security Responses**

* Temporary account lock

* Forced MFA

* Immediate logout

* Admin alert

* Report into Security Events panel

# **CHAPTER 29 – ANALYTICS & BI DASHBOARDS**

The Admin Panel must include real-time Business Intelligence dashboards.

## **29.1 Key Metrics**

### **Flights**

* Total bookings

* Revenue by route

* Airline performance

* Cancellation rates

### **Cars**

* Popular routes

* Trip counts

* Driver performance

### **Hotels**

* Most-booked cities

* Average price per night

### **Visas**

* Country demand

* Processing delays

* Approval/rejection rates

### **Users**

* Active vs new users

* Agent performance

## **29.2 Dashboard Components**

* Line charts

* Bar charts

* Geographic heat maps

* Pie charts

* Tabular analytics

* Export (PDF/CSV)

* Scheduled reports

# **CHAPTER 30 – FILE STORAGE (BACKBLAZE B2)**

All uploaded documents must be stored securely in Backblaze.

## **30.1 File Categories**

* Tickets

* Invoices

* Visa results

* Payment receipts

* User documents

* Hotel images

* Car images

## **30.2 Storage Requirements**

* Signed URLs for private access

* Expirable links

* Bucket + folder structure

* Daily backup of critical documents

* Access control based on user role

Continuing with **multiple full chapters per message**, fully detailed and formatted for the Implementation Agent.

No summaries. No interruptions. The providercript continues.

# **CHAPTER 31 – CI/CD PIPELINES & AUTOMATED DELIVERY**

NOVAX TRAVEL requires a fully automated software delivery process using GitHub Actions for all repositories.

## **31.1 Repositories**

the Implementation Agent must create and configure:

1. **backend-api** (Laravel)

2. **web-portal** (Next.js)

3. **admin-panel** (Next.js)

4. **mobile-app** (Flutter)

5. **infrastructure-config** (env templates, IaC if used)

## **31.2 Backend CI/CD Pipeline**

Pipeline automation must:

1. Run PHPUnit tests

2. Perform code linting

3. Validate migrations

4. Build production package

5. Deploy to Render via API key

6. Invalidate Cloudflare cache

7. Notify Admin via email/push message

## **31.3 Web Portal CI/CD Pipeline (Next.js)**

Pipeline tasks:

* Install dependencies

* TypeScript checks

* Lint & format

* Build Next.js production bundle

* Deploy to Vercel

* Invalidate Cloudflare cache

* Send deployment summary

## **31.4 Admin Panel CI/CD Pipeline**

Identical to Web, with additional checks:

* Admin routes protection

* RBAC integrity test

* Permission matrix validation

## **31.5 Mobile App CI/CD**

Flutter pipeline must:

* Run formatter

* Run analyzer

* Build APK (Release)

* Upload to Backblaze B2 (OTA system)

* Generate version metadata

* Notify users via push notification when new version is available

## **31.6 Environment Management**

the Implementation Agent must define:

* `.env.example` for each repo

* Secure secrets in GitHub

* Production vs staging variables

* Neon database branch isolation

# **CHAPTER 32 – CLOUD INFRASTRUCTURE & DEPLOYMENT TOPOLOGY**

A stable, low-cost, high-performance infrastructure is required.

## **32.1 Infrastructure Providers**

* **Database**: Neon PostgreSQL

* **Backend hosting**: Render

* **Web/Admin hosting**: Vercel

* **Object storage**: Backblaze B2

* **DNS + WAF + SSL**: Cloudflare

* **Notifications**: Firebase FCM / SMTP

## **32.2 Infrastructure Diagram**

```

[ Cloudflare DNS + WAF + SSL

]

|

|                                              |

[ Vercel: Web Portal ]                        [ Vercel: Admin Panel ]

|                                              |

------------------- [ Laravel API – Render ]  |

|

|

[ Neon PostgreSQL ]

|

[ Backups ]

|

[ Backblaze B2 ]

|

[ Flutter App ]

|

[ FCM Push Notifications ]

```

## **32.3 Infrastructure Requirements**

* Global CDN caching for Web

* WAF filtering for all traffic

* Forced SSL

* Multi-region DB read replicas (future-ready)

* Daily storage integrity scans

* API latency < 500ms (target, not enforced)

# **CHAPTER 33 – CLOUDFLARE CONFIGURATION**

Cloudflare acts as the **security and performance shield** for NOVAX TRAVEL.

## **33.1 DNS Setup**

* A records for backend

* CNAME for Web & Admin pointing to Vercel

* CNAME for asset domains

## **33.2 SSL/TLS Configuration**

* Full (Strict) mode

* HSTS enabled

* TLS 1.2+ only

* Disable insecure cipher suites

## **33.3 WAF Rules**

Rules must block:

* SQL injection patterns

* XSS attempts

* Path traversal

* High-frequency API calls (rate limit)

* Suspicious country-based access (optional)

* Scripted bots

## **33.4 Firewall Policies**

* Block non-HTTPS

* Block TOR access

* Geo-block optional regions

* Challenge unknown ASN traffic

## **33.5 Bot Protection**

Enable:

* Bot Fight Mode

* JS Challenge for suspicious traffic

# **CHAPTER 34 – BACKUP, RESTORE & PITR STRATEGY**

NOVAX TRAVEL must follow enterprise-grade data protection standards.

## **34.1 Database Backup Requirements**

* Daily automatic backups

* Weekly full backups

* Point-in-time recovery (PITR) enabled on Neon

* Backup retention: minimum 30 days

* Offsite redundancy

## **34.2 Storage Backup Requirements**

* Critical user documents backed up daily

* Redundant bucket replication (if supported)

## **34.3 Configuration Backup**

Must include:

* Pricing rules

* RBAC structure

* Agencies data

* Corporate accounts

* System settings

* Notification templates

Stored as encrypted JSON snapshots.

## **34.4 Restore Strategy**

Restoration must support:

* Full DB restore

* Point-in-time restore

* Single-table restore (via staging environment)

* Document restoration via Backblaze versioning

# **CHAPTER 35 – DISASTER RECOVERY & INCIDENT RESPONSE**

A robust recovery workflow is essential.

## **35.1 Disaster Types to Cover**

* Database corruption

* Render service downtime

* Vercel outage

* Backblaze bucket failure

* Cloudflare routing issues

* Security breach

* Credential leak

## **35.2 Incident Response Workflow**

```

[DETECT]

↓

[CONTAIN]

↓

[ANALYZE]

↓

[SOLVE]

↓

[RESTORE]

↓

[REPORT]

↓

[PREVENT RECURRENCE]

```

## **35.3 Automatic Safety Mechanisms**

* Auto-lock user accounts after suspected breach

* Auto-revoke tokens system-wide

* Force MFA reset

* Admin alerts

* Emergency maintenance mode activation

## **35.4 Disaster Recovery Objectives**

* **RTO (Recovery Time Objective):** As fast as possible; no fixed times.

* **RPO (Recovery Point Objective):** Minimal data loss due to PITR.

# **CHAPTER 36 – OTA (OVER-THE-AIR) UPDATE SYSTEM**

NOVAX TRAVEL’s mobile app must update

automatically without Play Store.

## **36.1 Update Workflow**

1. New APK built via CI/CD

2. Uploaded to Backblaze

3. Version metadata updated

4. App detects new version

5. User prompted to install

## **36.2 Offline Update Handling**

If offline:

* App stores metadata

* Installs once online

## **36.3 Admin Panel Integration**

Admin Panel must show:

* Current release version

* Release notes

* Force update toggle

# **CHAPTER 37 – SERVICE LEVEL RULES (SLA ENGINE)**

Every request type must have SLA rules.

## **37.1 SLA Examples**

* Ticket issuance within X steps (configurable)

* Visa processing SLA based on country

* Car assignment within 1 hour (configurable)

* Payment verification escalates if exceeds threshold

* Admin alert on SLA breaches

## **37.2 SLA Monitoring Dashboard**

Must display:

* Open SLA breaches

* Upcoming deadlines

* Team member workload

* Request distribution by state

# **CHAPTER 38 – SYSTEM SETTINGS & CONFIGURATION MANAGEMENT**

All system-level configurations must be editable via the Admin Panel.

## **38.1 Branding Controls**

* Logo

* Colors

* Email template styling

* Ticket/Invoice templates

## **38.2 Feature Toggles**

* Enable/Disable flight module

* Enable/Disable car service

* Enable/Disable visa system

* Enable/Disable guest mode

* Enable/Disable notifications

## **38.3 Pricing Controls**

* Default markups

* Seasonal adjustments

* Agent-specific overrides

## **38.4 Security Controls**

* Password policy

* MFA policy

* Session TTL configuration

* IP allow/block lists

## **38.5 Maintenance Mode**

Admin can:

* Activate maintenance

* Show custom message

* Allow specific IPs

# **CHAPTER 39 – ACCEPTANCE CRITERIA FOR IMPLEMENTATION AGENT DELIVERY**

the Implementation Agent must deliver a **fully working system** with:

* Backend deployed

* Web portal deployed

* Admin panel deployed

* Mobile app built + OTA ready

* Database seeded

* Pricing engine functional

* SLA engine working

* Notifications operating

* Full RBAC applied

* Full Yemen dataset seeded

* Admin account created

* Documentation generated

* Runbook provided

* Environment variables injected

## **39.1 Required Artifacts**

the Implementation Agent must produce:

* Source code for all systems

* DB schema export

* Admin credentials

* User manual

* Deployment manual

* API documentation

* System architecture document

## **39.2 Final Delivery Validation**

System must run:

* Without errors

* Without missing features

* Without manual coding

* With all workflows operational

# **CHAPTER 40 – GLOSSARY & DEFINITIONS**

* **API**: Application Programming Interface

* **B2**: Backblaze storage system

* **RBAC**: Role-Based Access Control

* **SLA**: Service Level Agreement

* **MFA**: Multi-Factor Authentication

* **IDS**: Intrusion Detection System

* **OTA**: Over-the-Air Update

* **PITR**: Point-in-Time Recovery

* **KPI**: Key Performance Indicator

* **WAF**: Web Application Firewall

* **CDN**: Content Delivery Network

* **JWT**: JSON Web Token

Continuing the providercript with **multiple complete chapters**, adding deep technical detail, tables, diagrams, JSON structures, admin screen definitions, and final the Implementation Agent execution mandate.

We proceed.

# **CHAPTER 41 – APPENDIX A: FULL YEMEN GOVERNORATES & CITIES DATASET**

This appendix provides a **complete baseline dataset** to be seeded by the Implementation Agent into the PostgreSQL database.

The dataset must support **offline mobile operation**, domestic flight search, and location-based services.

## **41.1 Governorates Dataset (JSON Seed Format)**

```

[

{ "id": 1, "name_ar": "أمانة العاصمة", "name_en": "Amanat Al-Asimah (Sana’a City)", "capital_en": "Sana’a" },

{ "id": 2, "name_ar": "صنعاء", "name_en": "Sana’a", "capital_en": "Sana’a" },

{ "id": 3, "name_ar": "عدن", "name_en": "Aden", "capital_en": "Aden" },

{ "id": 4, "name_ar": "تعز", "name_en": "Taiz", "capital_en": "Taiz" },

{ "id": 5, "name_ar": "لحج", "name_en": "Lahj", "capital_en": "Lahj" },

{ "id": 6, "name_ar": "أبين", "name_en": "Abyan", "capital_en": "Zinjibar" },

{ "id": 7, "name_ar": "شبوة", "name_en": "Shabwah", "capital_en": "Ataq" },

{ "id": 8, "name_ar": "حضرموت", "name_en": "Hadhramaut", "capital_en": "Mukalla" },

{ "id": 9, "name_ar": "المهرة", "name_en": "Al Mahrah", "capital_en": "Al Ghaidah" },

{ "id": 10, "name_ar": "مأرب", "name_en": "Marib", "capital_en": "Marib" },

{ "id": 11, "name_ar": "الجوف", "name_en": "Al Jawf", "capital_en": "Al Hazm" },

{ "id": 12, "name_ar": "صعدة", "name_en": "Sa’dah", "capital_en": "Sa’dah" },

{ "id": 13, "name_ar": "عمران", "name_en": "Amran", "capital_en": "Amran" },

{ "id": 14, "name_ar": "ذمار", "name_en": "Dhamar", "capital_en": "Dhamar" },

{ "id": 15, "name_ar": "إب", "name_en": "Ibb", "capital_en": "Ibb" },

{ "id": 16, "name_ar": "ريمة", "name_en": "Raymah", "capital_en": "Raymah" },

{ "id": 17, "name_ar": "البيضاء", "name_en": "Al Bayda", "capital_en": "Al Bayda" },

{ "id": 18, "name_ar": "الحديدة", "name_en": "Al Hudaydah", "capital_en": "Al Hudaydah" },

{ "id": 19, "name_ar": "المحويت", "name_en": "Al Mahwit", "capital_en": "Al Mahwit" },

{ "id": 20, "name_ar": "حجة", "name_en": "Hajjah", "capital_en": "Hajjah" },

{ "id": 21, "name_ar": "الضالع", "name_en":

"Al Dhale’e", "capital_en": "Al Dhale’e" },

{ "id": 22, "name_ar": "سقطرى", "name_en": "Socotra", "capital_en": "Hadibo" }

]

```

## **41.2 Airport Cities Dataset**

Must be preloaded into `yemen_cities`:

```

[

{ "id": 101, "city_en": "Sana’a", "type": "airport_city", "airport_code": "SAH" },

{ "id": 102, "city_en": "Aden", "type": "airport_city", "airport_code": "ADE" },

{ "id": 103, "city_en": "Seiyun", "type": "airport_city", "airport_code": "GXF" },

{ "id": 104, "city_en": "Riyan (Mukalla)",

"type": "airport_city", "airport_code": "RIY" },

{ "id": 105, "city_en": "Al Ghaidah", "type": "airport_city", "airport_code": "AAY" },

{ "id": 106, "city_en": "Socotra", "type": "airport_city", "airport_code": "SCT" },

{ "id": 107, "city_en": "Taiz", "type": "airport_city", "airport_code": "TAI" },

{ "id": 108, "city_en": "Al Hudaydah", "type": "airport_city", "airport_code": "HOD" }

]

```

## **41.3 Airline Dataset**

*(Minimum required Yemeni carriers)*

```

[

{ "id": 1, "name_en": "Yemenia Airways",

"iata": "IY", "icao": "IYE" },

{ "id": 2, "name_en": "Felix Airways (Al Saeeda)", "iata": "FF", "icao": "FXX" },

{ "id": 3, "name_en": "Queen Bilqis Airways", "iata": "QB", "icao": "QBA" },

{ "id": 4, "name_en": "Aden Airways", "iata": "AD", "icao": "ADN" },

{ "id": 5, "name_en": "Private Charter Carrier", "iata": "--", "icao": "--" }

]

```

## **41.4 Sample Yemen Domestic Routes (Seed Data)**

```

[

{ "origin": "Seiyun", "destination": "Jeddah", "airline_id": 1 },

{ "origin": "Seiyun", "destination": "Cairo", "airline_id": 1 },

{ "origin": "Aden", "destination": "Jeddah", "airline_id": 1 },

{ "origin": "Aden", "destination": "Riyadh", "airline_id": 3 },

{ "origin": "Riyan", "destination": "Cairo", "airline_id": 1 },

{ "origin": "Ghaidah", "destination": "Amman", "airline_id": 1 }

]

```

# **CHAPTER 42 – APPENDIX B: FULL ADMIN PANEL SCREEN BLUEPRINT**

Below is the **complete hierarchy of

screens** the Implementation Agent must build inside the Admin Panel (Next.js).

## **42.1 Dashboard Screens**

* System KPIs

* Active requests panel

* SLA alerts

* Security alerts

* Recent activity logs

* Revenue graph

* Agent performance ranking

## **42.2 User & Access Screens**

**Users**

* List users

* Create user

* Edit user

* Assign roles

* Activate/Deactivate

**Roles & Permissions**

* List roles

* Create role

* Assign permissions

* Permission matrix view

## **42.3 Agencies & Corporate Screens**

**Agencies**

* Agency list

* Create agency

* Set commissions

* View financials

* Manage sub-agents

* Monthly statements

**Corporate Accounts**

* Company list

* Employees list

* Spending rules

* Manager approvals

* Pricing overrides

## **42.4 Travel Service Modules (Each with full CRUD)**

### **Flights**

* Domestic schedules

* Manual flight creation

* Fare rules

* Upload tickets

* Route activation

### **Hotels**

* Hotel list

* Room management

* Amenities

* Price overrides

### **Cars**

* Drivers

* Vehicles

* Routes

* Pricing rules

### **Visas**

* Visa country list

* Required documents

* Processing steps

* Price configurations

## **42.5 Pricing & Commission Engine UI**

* List pricing rules

* Create pricing rule

* Priority levels

* Rule simulation tester

* Agent override pricing

* Seasonal pricing editor

* Service bundle rules editor

## **42.6 Requests Engine UI**

* List all requests

* Filter by state

* SLA indicator

* Approve / Reject

* Upload ticket

* Payment verification

* Notes and internal chat

## **42.7 Notifications UI**

* Notification template editor

* Email templates

* Push templates

* In-app message templates

* Test-send tool

## **42.8 System Settings UI**

* Branding

* Logos

* Primary colors

* Maintenance mode toggle

* Feature flags

* MFA enforcement configuration

* IP Allow/Block lists

## **42.9 Audit & Security UI**

* Audit logs viewer

* Security events log

* Login attempts

* IDS alerts

* IP reputation checks

## **42.10 OTA Update Center**

* Upload APK

* View versions

* Force update toggle

* Release notes

# **CHAPTER 43 – APPENDIX C: SAMPLE API ENDPOINT CATALOG**

the Implementation Agent must generate the full backend API, but below is a required baseline catalog.

## **43.1 Authentication API**

```

POST /auth/register

POST /auth/login

POST /auth/logout

POST /auth/refresh

POST /auth/mfa/enable

POST /auth/mfa/verify

```

## **43.2 Flight API**

```

GET /flights/search

POST /flights/manual/create

GET /flights/routes

POST /flights/ticket/upload

```

## **43.3 Request Engine**

```

POST /requests/create

GET /requests/{id}

POST /requests/{id}/state/change

POST /requests/{id}/payment/verify

```

## **43.4 Pricing Engine**

```

GET /pricing/rules

POST /pricing/rules/create

POST /pricing/rules/apply

```

## **43.5 Agencies**

```

GET /agencies

POST /agencies/create

GET /agencies/{id}/balance

POST /agencies/{id}/commission

```

## **43.6 Wallet & Loyalty**

```

GET /wallet

POST /wallet/credit

POST /wallet/debit

GET /loyalty

```

# **CHAPTER 44 – APPENDIX D: OFFLINE MOBILE SYNC ENGINE**

## **44.1 Architecture**

```

[Local DB] <--> [Sync Queue] <--> [Background Sync Worker] <--> [API]

```

## **44.2 Sync Priorities**

1. Authentication & tokens

2. Yemen dataset

3. Pricing rules

4. User requests

5. Notifications

6. Offline-created booking requests

## **44.3 Conflict Resolution**

Rules:

* Server wins for pricing and schedules

* Client keeps local drafts

* Merge payloads when possible

# **CHAPTER 45 – APPENDIX E: SAMPLE

SYSTEM DIAGRAMS**

## **45.1 End-to-End User Request Flow**

```

[User]

|

v

[Search Flights]

|

v

[Select Flight]

|

v

[Submit Request]

|

v

[Admin Review]

|

+--> [Reject]

|

v

[Payment Upload]

|

v

[Finance Verification]

|

v

[Ticket Issued]

|

v

[Completed]

```

## **45.2 Admin Panel Routing Architecture**

```

/dashboard

/users

/roles

/agencies

/corporate

/flights

/hotels

/cars

/visas

/requests

/pricing

/commissions

/notifications

/settings

/security

/ota

```

# **CHAPTER 46 – APPENDIX F: SAMPLE JSON STRUCTURES**

## **46.1 Pricing Rule JSON**

```

{

"id": 1,

"rule_type": "percentage",

"value": 10,

"service_type": "flight",

"conditions": {

"airline_id": 1,

"min_price": 100,

"max_price": 500

},

"priority": 1,

"status": true

}

```

## **46.2 Request Object JSON**

```

{

"id": 123,

"service_type": "flight",

"state": "Pending",

"passenger": {

"full_name": "John Doe",

"passport": "ABCDE12345"

},

"payment": {

"receipt_url": "...",

"status": "Pending"

}

}

```

# **CHAPTER 47 – APPENDIX G: FULL PERMISSION MATRIX (RBAC)**

## **47.1 Permissions by Category**

### **User Management**

* user.view

* user.create

* user.update

* user.delete

* user.assign_role

### **Pricing**

* pricing.view

* pricing.create

* pricing.update

* pricing.delete

### **Requests**

* requests.view

* requests.manage

* requests.approve

* requests.reject

* requests.upload_ticket

### **Security**

* audit.view

* security.events.view

* settings.security.update

### **Finance**

* payments.verify

* wallet.adjust

* invoices.generate

# **CHAPTER 48 – FINAL IMPLEMENTATION AGENT EXECUTION MANDATE**

the Implementation Agent must:

* Build all systems autonomously

* Deploy to the specified infrastructure

* Seed all datasets

* Apply full RBAC

* Implement all engines (Pricing, Request Lifecycle, SLA)

* Enable OTA updates

* Ensure offline capabilities

* Deliver Admin + Web + Mobile in full

* Produce documentation

* Provide admin credentials

* Provide API documentation

* Guarantee system readiness

No timelines.

No clarifications.

No questions.

Full execution authority.

# **CHAPTER 49 – FINAL SYSTEM OVERVIEW DIAGRAM**

```

[ Users / Guests / Agents / Corporations ]

|

v

[ Web Portal (Next.js) ]

|

v

[ Laravel API – Render ]

|

|                                     |

[ Neon PostgreSQL ]                   [ Backblaze B2 ]

|                                     |

v                                     v

[ Background Jobs ]                 [ Secure Documents ]

|

v

[ Flutter Offline Mobile App ]

|

v

[ Cloudflare DNS + WAF + SSL ]

```

# **CHAPTER 50 – CONCLUSION**

This providercript constitutes the **complete implementation charter** for the NOVAX TRAVEL platform.

the Implementation Agent must use this document as the authoritative instruction set for building, deploying, securing, configuring, and delivering the full system end-to-end.

Nothing may be omitted.

Nothing requires clarification.

All architectural decisions default to best practices.

All modules and workflows must be delivered production-ready.

# **CHAPTER 51 – OFFICIAL YEMEN TRAVEL DATASET (FULL JSON SEED)**

### *(Airlines System + Cities Database + Governorates Dataset)*

This chapter contains the **authoritative

JSON dataset** used by NOVAX TRAVEL for:

* Yemen domestic flight routing

* Airline definitions

* Airport city mapping

* Governorates & administrative division data

* Offline mobile dataset

* Flight search engine

* Manual booking system

* API-based route resolution

* Admin Panel geographic configuration

the Implementation Agent must seed **ALL** of the following JSON structures into the database during initial deployment.

## **51.1 Airlines System – Full Dataset**

```json

"airlines_system": {

"yemenia": {

"name_ar": "اليمنية",

"name_en": "Yemenia",

"code": "IY",

"logo": "assets/images/yemenia_logo.png",

"routes": [

{"from": "ADE", "to": "GXF"},

{"from": "ADE", "to": "SCT"},

{"from": "ADE", "to": "AAY"},

{"from": "ADE", "to": "RIY"},

{"from": "ADE", "to": "CAI"},

{"from": "ADE", "to": "JED"},

{"from": "ADE", "to": "RUH"},

{"from": "ADE", "to": "AMM"},

{"from": "ADE", "to": "KRT"},

{"from": "ADE", "to": "ADD"},

{"from": "ADE", "to": "JIB"},

{"from": "ADE", "to": "DXB"},

{"from": "ADE", "to": "BOM"},

{"from": "ADE", "to": "KWI"},

{"from": "ADE", "to": "DOH"},

{"from": "GXF", "to": "ADE"},

{"from": "GXF", "to": "CAI"},

{"from": "GXF", "to": "JED"},

{"from": "SCT", "to": "ADE"},

{"from": "SCT", "to": "AAY"},

{"from": "SCT", "to": "RIY"},

{"from": "RIY", "to": "ADE"},

{"from": "RIY", "to": "SCT"},

{"from": "RIY", "to": "DXB"},

{"from": "RIY", "to": "CAI"},

{"from": "RIY", "to": "JED"},

{"from": "AAY", "to": "ADE"},

{"from": "AAY", "to": "SCT"},

{"from": "AXK", "to": "ADE"}

]

},

"queen_bilqis": {

"name_ar": "طيران الملكة بلقيس",

"name_en": "Queen Bilqis Airways",

"code": "QB",

"logo": "assets/images/queen_bilqis_logo.png",

"routes": [

{"from": "ADE", "to": "CAI"},

{"from": "CAI", "to": "ADE"}

]

},

"aden_air": {

"name_ar": "طيران عدن",

"name_en": "Aden Air",

"code": "AD",

"logo": "assets/images/aden_air_logo.png",

"routes": [

{"from": "ADE", "to": "CAI"},

{"from": "CAI", "to": "ADE"}

]

}

}

```

## **51.2 Cities Database – Full Dataset**

```json

"cities_database": [

{"id": "ADE", "name_ar": "عدن", "name_en": "Aden", "type": "domestic", "country": "YE"},

{"id": "GXF", "name_ar": "سيئون", "name_en": "Seiyun", "type": "domestic", "country": "YE"},

{"id": "SCT", "name_ar": "سقطرى",

"name_en": "Socotra", "type": "domestic", "country": "YE"},

{"id": "AAY", "name_ar": "الغيضة", "name_en": "Al Ghaydah", "type": "domestic", "country": "YE"},

{"id": "RIY", "name_ar": "الريان المكلا", "name_en": "Riyan Mukalla", "type": "domestic", "country": "YE"},

{"id": "AXK", "name_ar": "عتق", "name_en": "Ataq", "type": "domestic", "country": "YE"},

{"id": "CAI", "name_ar": "القاهرة", "name_en": "Cairo", "type": "international", "country": "EG"},

{"id": "JED", "name_ar": "جدة", "name_en": "Jeddah", "type": "international", "country": "SA"},

{"id": "RUH", "name_ar": "الرياض", "name_en": "Riyadh", "type": "international", "country": "SA"},

{"id": "AMM", "name_ar": "عمّان", "name_en":

"Amman", "type": "international", "country": "JO"},

{"id": "KRT", "name_ar": "الخرطوم", "name_en": "Khartoum", "type": "international", "country": "SD"},

{"id": "ADD", "name_ar": "أديس أبابا", "name_en": "Addis Ababa", "type": "international", "country": "ET"},

{"id": "JIB", "name_ar": "جيبوتي", "name_en": "Djibouti", "type": "international", "country": "DJ"},

{"id": "DXB", "name_ar": "دبي", "name_en": "Dubai", "type": "international", "country": "AE"},

{"id": "BOM", "name_ar": "بومباي", "name_en": "Bombay", "type": "international", "country": "IN"},

{"id": "KWI", "name_ar": "الكويت", "name_en": "Kuwait", "type": "international", "country": "KW"},

{"id": "DOH", "name_ar": "الدوحة",

"name_en": "Doha", "type": "international", "country": "QA"}

]

```

## **51.3 Governorates Dataset – Full List**

```json

{

"governorates": [

{ "id": 1, "name_ar": "أبين", "name_en": "Abyan", "capital_ar": "زنجبار", "capital_en": "Zinjibar" },

{ "id": 2, "name_ar": "أمانة العاصمة", "name_en": "Amanat Al Asimah (Sana'a City)", "capital_ar": "صنعاء", "capital_en": "Sana'a" },

{ "id": 3, "name_ar": "إب", "name_en": "Ibb",

"capital_ar": "إب", "capital_en": "Ibb" },

{ "id": 4, "name_ar": "البيضاء", "name_en": "Al Bayda", "capital_ar": "البيضاء", "capital_en": "Al Bayda" },

{ "id": 5, "name_ar": "الحديدة", "name_en": "Al Hudaydah", "capital_ar": "الحديدة", "capital_en": "Al Hudaydah" },

{ "id": 6, "name_ar": "الجوف", "name_en": "Al Jawf", "capital_ar": "الحزم", "capital_en": "Al Hazm" },

{ "id": 7, "name_ar": "المحويت", "name_en": "Al Mahwit", "capital_ar": "المحويت", "capital_en": "Al Mahwit" },

{ "id": 8, "name_ar": "المهرة", "name_en": "Al Mahrah", "capital_ar": "الغيضة", "capital_en": "Al Ghaydah" },

{ "id": 9, "name_ar": "الضالع", "name_en": "Ad Dali'", "capital_ar": "الضالع", "capital_en": "Ad Dali'" },

{ "id": 10, "name_ar": "حجة", "name_en": "Hajjah", "capital_ar": "حجة", "capital_en":

"Hajjah" },

{ "id": 11, "name_ar": "حضرموت", "name_en": "Hadramawt", "capital_ar": "المكلا", "capital_en": "Mukalla" },

{ "id": 12, "name_ar": "ريمة", "name_en": "Raymah", "capital_ar": "الجبين", "capital_en": "Al Jabin" },

{ "id": 13, "name_ar": "شبوة", "name_en": "Shabwah", "capital_ar": "عتق", "capital_en": "Ataq" },

{ "id": 14, "name_ar": "صعدة", "name_en": "Sa'dah", "capital_ar": "صعدة", "capital_en": "Sa'dah" },

{ "id": 15, "name_ar": "صنعاء", "name_en": "Sana'a", "capital_ar": "صنعاء", "capital_en": "Sana'a" },

{ "id": 16, "name_ar": "تعز", "name_en": "Taizz", "capital_ar": "تعز", "capital_en": "Taizz" },

{ "id": 17, "name_ar": "عدن", "name_en": "Aden", "capital_ar": "عدن", "capital_en":

"Aden" },

{ "id": 18, "name_ar": "عمران", "name_en": "Amran", "capital_ar": "عمران", "capital_en": "Amran" },

{ "id": 19, "name_ar": "لحج", "name_en": "Lahij", "capital_ar": "الحوطة", "capital_en": "Al Houta" },

{ "id": 20, "name_ar": "مأرب", "name_en": "Ma'rib", "capital_ar": "مأرب", "capital_en": "Ma'rib" },

{ "id": 21, "name_ar": "سقطرى", "name_en": "Socotra", "capital_ar": "حديبو", "capital_en": "Hadibu" },

{ "id": 22, "name_ar": "ذمار", "name_en": "Dhamar", "capital_ar": "ذمار", "capital_en": "Dhamar" }

],

"meta": {

"count": 22,

"source": "Yemeni administrative division",

"note": "Socotra is officially an archipelago and governorate. Some sources may list 21 governorates by grouping it with Hadramawt."

}

}

```

Continuing the providercript with multiple fully detailed chapters expanding the Yemen dataset, its intelligence layers, search optimization, API normalization, and international scalability.

We proceed.

CHAPTER 57 – DATA MATCHING BETWEEN AIRLINES, CITIES & GOVERNORATES

NOVAX TRAVEL must maintain strict relational consistency between:

Airlines

Routes

Cities

Governorates

This chapter defines the validation and alignment logic required for stable operations.

57.1 City–Governorate Binding Rule

Every city must be mapped to exactly one governorate.

Validation Process:

Lookup city.id

Determine governorate using static table

Assign governorate_id

Enforce NOT NULL constraint

Reject inconsistent dataset updates

Example:

City: Aden (ADE) Governorate: Aden → governorate_id = 17

57.2 Route–City Integrity Rule

For every route:

origin_city_id MUST exist in yemen_cities

destination_city_id MUST exist in yemen_cities

airline_id MUST exist in airlines

If any fails:

route is quarantined

integrity alert is logged in audit

Admin sees warning in Data Integrity Center

57.3 Route–Airport Code Conversion

Airlines define routes using IATA codes.

System must convert these codes to internal IDs.

Example:

Input: { "from": "ADE", "to": "CAI" } Internal mapping: origin_city_id = ADE destination_city_id = CAI country_codes applied domestic/international flags assigned

57.4 Airline–Route Synchronization Rule

If an airline is deactivated:

All routes must be soft-deactivated

Users cannot book flights for those routes

Mobile offline dataset must remove or gray-out routes

57.5 Automatic Reverse Route Matching

For each:

{ from: X, to: Y }

System must create reverse route:

{ from: Y, to: X }

unless flagged as one-directional.

CHAPTER 58 – FULL-TEXT SEARCH INDEXES FOR YEMEN DATA

The NOVAX TRAVEL search engine must support high-performance text lookups for:

Cities

Governors

Countries

Airlines

Routes

This chapter defines PostgreSQL FTS configuration.

58.1 Required Search Fields

Cities:

name_ar

name_en

airport_code

governorate_name

Airlines:

name_ar

name_en

code

Routes:

origin_city_name

destination_city_name

airline code/name

58.2 PostgreSQL FTS Index Creation

Example index for cities:

CREATE INDEX idx_city_search ON yemen_cities USING GIN (to_tsvector('simple', name_en || ' ' || name_ar || ' ' || airport_code));

Example index for airlines:

CREATE INDEX idx_airline_search ON airlines USING GIN (to_tsvector('simple',

name_en || ' ' || name_ar || ' ' || code));

58.3 Mobile Offline Search Index

Mobile must generate an offline FTS dictionary:

normalized Arabic

simplified English

airport codes

synonyms (Mukalla → Riyan, etc.)

58.4 Search Ranking Formula

score = (exact match * 3) + (airport code match * 2) + (partial match * 1) + (governorate match * 0.5)

58.5 Special Yemen Search Rules

These apply due to naming inconsistencies:

"Mukalla" must match both "Mukalla" and "Riyan"

"Seyun" must match "Seiyun" and "Seyoun"

"Socotra" must match "Sokotora", "Sokotra", "Suctra", "سقطرى"

CHAPTER 59 – INTERNATIONAL EXPANSION DATA MODEL

NOVAX TRAVEL must be built for Yemen first but globally scalable.

This chapter defines how to expand from Yemen → Global.

59.1 Expansion Entities

Global support requires:

Expanded cities database

Global airport database (IATA)

Country table

Timezone table

Global airline database

Global route table (API-based)

59.2 Future API Integrations

Designed to integrate:

Duffel

TravelPayouts

Amadeus (future)

Kiwi/Tequila (future)

59.3 Global Dataset Structure

global_airports: id name city country_code iata icao latitude longitude timezone

59.4 Global Normalization Rules

If airport exists both in Yemen dataset & global dataset → merge records.

Prefer IATA-based uniqueness.

Regional aliasing must be added for multi-named cities.

Global routes will override manual ones when API-enabled.

CHAPTER 60 – API

NORMALIZATION RULES FOR FUTURE GLOBAL PROVIDERS

Although Yemen routes are manual, the system must support future API-based global expansion.

60.1 API Input Normalization

Global APIs return fields like:

origin: "CAI" destination: "DXB" airline: "EK" iata_flight_number: "EK924" price: 230.5

These must be normalized into internal schema:

origin_city_id = CAI destination_city_id = DXB airline_id = lookup("EK") fare_base = price fare_display = pricing_engine(price) is_domestic = false

60.2 API–Manual Merge Logic

If global API is enabled:

results = merge(manual_domestic_flights,

global_api_results)

Manual Yemen flights always have priority for:

local display

domestic pricing rules

offline mode

SLA calculations

60.3 Error Tolerance Rules

If API fails:

return only manual flights

fallback to cached API results (up to 24 hours)

log failure in audit

CHAPTER 61 – YEMEN ROUTE NORMALIZATION & CLEANING ENGINE

This chapter defines how the Implementation Agent must automatically clean, fix, normalize, and enrich Yemen routes.

61.1 Normalization Steps

Trim all whitespace

Convert city IDs to uppercase

Validate that both airports exist

Generate reverse routes

Add airline references

Add domestic/international flags

Ensure no circular routes (ADE → ADE)

Enforce unique constraint (no duplicates)

61.2 Route Cleaning Examples

Input:

{ "from": " ade ", "to": " cai " }

Normalized:

{ "from": "ADE", "to": "CAI" }

61.3 Automatic Missing Data Correction

If duration missing → estimate using distance:

duration = distance_km / 650 km/h

If route price undefined → use default airline markup.

CHAPTER 62 – AIRPORT DISTANCE CALCULATION ENGINE

These distances are required for:

Estimated duration

Fuel-based route scoring (future)

Load prediction models

62.1 Haversine Formula (Required)

distance = 2 * R * arcsin( sqrt( sin²((lat2 - lat1)/2) + cos(lat1) * cos(lat2) * sin²((lon2 - lon1)/2) ))

R = 6371 km

62.2 Store Distances Per Route

New table:

route_distances: origin_city_id destination_city_id distance_km duration_estimated

62.3 Use in Search Engine

Sort flights by:

price

duration

shortest route

CHAPTER 63 – SEASONAL PATTERN ENGINE FOR YEMEN ROUTES

Yemeni travel demand is highly seasonal.

63.1 Required Seasons

Ramadan

Summer peak

Hajj

Umrah seasons

Winter low season

63.2 Route Seasonal Multiplier

Adjusted Price = Base Price * (1 + season_multiplier)

Examples:

Ramadan: +15%

Summer: +10%

Winter: -5%

63.3 Admin Panel Seasonal Dashboard

Admin can:

Create seasons

Apply airlines

Apply routes

Activate/deactivate

CHAPTER 71 – ADMIN-CONTROLLED GLOBAL

SYSTEM BUILDER

This chapter defines the master control layer of NOVAX TRAVEL:

Everything MUST be manageable through the Admin Panel, without programming.

This is the rule:

If anything exists in NOVAX TRAVEL, admin must be able to create, edit, delete, or configure it visually.

No SQL. No code. All UI-based.

71.1 Admin Must Control All Core Entities

Admin can create, edit, and delete:

Airlines

Routes

Cities

Governorates

Hotels

Car rentals

Visa destinations

Travel packages

Companies

Agents

User roles & permissions

Banners, themes, colors

Payment methods

Loyalty point rules

Currency exchange rates

Pricing rules

Commission rules

Seasons & surcharges

Flight slots

Airport states

Offline mobile dataset version

API keys & integrations

Data imports & exports

71.2 Admin-Controlled System Policies

Admin can turn ON/OFF:

Guest mode

Booking engine

Loyalty system

Agent commissions

Corporate accounts

Offline mode enforcement

API usage priority

Maintenance mode

Surge pricing

Seasonal pricing

Airport closures

Airline suspensions

Fraud-detection strictness

71.3 Admin-Controlled Emergency Switches

These real-time switches MUST exist:

1. Disable all bookings

2. Disable only international bookings

3. Disable only domestic bookings

4. Freeze all prices globally

5. Freeze agent commissions

6. Enable emergency routes only

7. Broadcast system-wide notifications

71.4 Admin Action Log (Audit Center)

Every admin action must be logged:

who did it

what was changed

before/after values

timestamp

IP address

device ID

With export and filtering tools.

CHAPTER 72 – ADMIN PANEL MASTER BUILDER (SCREEN-BY-SCREEN)

This chapter instructs the Implementation Agent to build the full navigable Admin Panel.

72.1 Main Admin Navigation

Dashboard Airlines Cities & Governorates Routes & Schedules Hotels Cars & Transport Visa Destinations Requests Engine Pricing Engine Commission Engine Seasons & Surcharges Agents & Companies RBAC & Permissions Users Payments Loyalty System Content Management System Settings API Keys & Integrations Data Integrity Center Audit Log Maintenance Tools

72.2 Airlines Management Screen

Admin can:

Create airline

Upload logo

Add IATA/ICAO code

Configure baggage rules

Set commissions

Set markups

Activate/deactivate airline

Import/export airline routes dataset

72.3 Routes Management Screen

Admin can:

Add route (origin → destination)

Set price rules

Set flight durations

Configure seasonal adjustments

Assign airlines

Toggle active/inactive

Auto-generate reverse route

Add airport slot times

Add operational constraints

72.4 Pricing Engine Screen

Admin controls:

Global markups

Airline-level markups

Route-level markups

Agent-level markups

Corporate custom price contracts

Seasonal multipliers

Special offers and discounts

Minimum and maximum price rules

72.5 Commission Engine Screen

Supports:

Airline-level commissions

Route-level overrides

Agent-tier multipliers

Corporate account adjustments

Bonus campaigns

72.6 RBAC & Permissions Screen

Admin can:

Define roles

Assign permissions via toggles

Create new permission groups

Clone roles

Disable or archive roles

Assign roles to users/companies

72.7 Maintenance Tools Screen

Contains:

System cache clear

Pricing recalculation

Route rebuild

Offline dataset refresh

Database consistency scan

Automated backups control

Emergency shutdown tools

CHAPTER 73 – SAFETY & RISK FACTOR ROUTING ENGINE (YEMEN-SPECIFIC)

Domestic Yemeni travel is subject to unique risk factors.

NOVAX TRAVEL must incorporate a routing safety layer to prevent unsafe bookings.

73.1 Route Risk Categories

Each route must have a risk score:

Weather risk

Airport state risk

Airline operational stability

Regional conflict risk

Historical cancellation ratio

73.2 Route Safety Score Formula

safety_score = weather_factor + airport_state_factor + airline_reliability_factor + region_factor - cancellation_factor

73.3 Preventive Booking Logic

If safety_score < 40:

System must warn user

Admin approval may be required

If < 20:

Booking automatically blocked

CHAPTER 74 – FUEL COST & DISTANCE MODEL (FUTURE-READY)

This chapter prepares NOVAX TRAVEL for advanced cost modeling, even if not immediately used.

74.1 Base Formula

fuel_cost = distance_km * fuel_burn_rate_per_km

74.2 Airline-Level Fuel Efficiency

Each airline can store:

fuel_efficiency_index

fleet type (Airbus, Boeing, etc.)

74.3 Use Cases

Predict future price trends

Estimate airline surcharges

Support dynamic pricing

CHAPTER 75 – TRAVEL DOCUMENTATION & COMPLIANCE RULES (YEMEN USERS)

Travelers from Yemen require special documentation depending on destination.

75.1 Documentation Table

DestinationRequiredSaudi ArabiaPassport + Visa or Umrah/Hajj visaEgyptPassport + (sometimes visa required)JordanPassport + Entry Visa (depends on category)DjiboutiVisa on arrivalIndiaE-VisaUAEEntry permit depending on type

75.2 Exemptions

Diplomatic passports

Official missions

Re-entry permits

75.3 Admin Documentation

Rules Builder

Admin can define:

Required documents

Expiration rules

Additional forms

Visa eligibility

75.4 User App Integration

Users must upload documents:

Passport

ID

Visa

Medical certificate (if required)

All validated automatically using OCR (future module).

CHAPTER 76 – ADMIN-CONTROLLED GLOBAL BUILDER MODE

This chapter instructs the Implementation Agent to allow the entire system to grow without coding.

Everything MUST be manageable from the Admin panel, including:

Adding new countries

Adding new cities

Adding new airlines

Adding new airports

Expanding route networks

Adding new providers (APIs)

Adding new service types

Adding new travel categories

Adding new currencies

Adding new loyalty calculation models

Adding new themes

Adding new companies and partners

76.1 The “Create Anything” Mechanism

Admin can create new system entities without developer intervention.

Example new entity:

"Cruise lines"

"Bus routes"

"Travel insurance"

Each entity inherits:

CRUD screens

Pricing framework

Commission framework

RBAC permissions

API-ready model

76.2 Entity Properties Builder

Admin defines:

Fields & data types

Relations

Rules

Pricing logic

Permissions

UI layout

76.3 Auto-Generated Database Tables

When admin creates an entity:

the Implementation Agent generates migrations

Updates backend API

Updates Admin UI

Updates mobile & web front-end

Updates roles/permissions

ALL automatically.

CHAPTER 77 – UNIVERSAL IMPORT/EXPORT ENGINE

NOVAX TRAVEL must provide a powerful data import/export system.

77.1 Supported Formats

JSON

CSV

XLSX

XML (future)

77.2 Admin Can Import

Airlines

Routes

Hotels

Cities

Governorates

Pricing tables

Agent lists

Visa rules

77.3 Validation Pipeline

Structural validation

Duplicate detection

Mapping missing relations

Preview before applying

Undo capability

77.4 Export Tools

Admin can export:

Full dataset

Partial dataset

Data snapshot for backups

Understood perfectly.

You want the **Admin Panel to become the CENTRAL “SUPER ENGINE”** of

NOVAX TRAVEL — fully autonomous, with the same power as a **database management system, DevOps platform, migration tool, ETL system, content manager, and configuration engine**, all without writing a single line of code.

The Admin Panel must be able to:

* Create / edit / delete ANY database table

* Add fields to tables

* Modify field types

* Add relationships (FKs)

* Build new modules (entities)

* Move the entire project to another server

* Export and import the entire database

* Rebuild the backend models/API routes

* Re-generate migrations automatically

* Create API keys and integrations

* Control CI/CD and deploy to another hosting

* Generate backups and restore them

* Clone environment (staging → production)

* Change branding, workflows, rules

* Enable/disable ANY system module

* Apply schema updates across all layers automatically

You want a **no-code / low-code system builder**, built INTO the Admin Panel itself.

I will now create **the final and most important chapters** that finish the Admin “Super Engine”.

We proceed.

# **CHAPTER 78 – THE ADMIN SUPER ENGINE (NO-CODE SYSTEM BUILDER)**

This chapter defines the **core concept**:

**The Admin Panel IS the database, the backend, the system architect, the DevOps, the migration tool, and the configuration engine.**

Everything must be possible WITHOUT writing SQL or code.

## **78.1 Admin Panel = Database Designer**

Admin can:

* Create new tables

* Delete tables

* Rename tables

* Clone tables

* Add/remove fields

* Change field types

* Add indexes

* Add constraints: UNIQUE, FK, NOT NULL

* Add relations (one-to-one, one-to-many, many-to-many)

* Mark fields as required or optional

* Add validation rules

This is effectively a **no-code DBMS** inside NOVAX.

## **78.2 Admin Panel = API Manager**

Whenever admin creates/edits a table:

* the Implementation Agent automatically updates backend models

* Generates REST endpoints

* Updates permissions

* Updates Admin screen forms & lists

* Updates mobile & web API contracts

The admin **never** sees the code—only the results.

## **78.3 Admin Panel = Migration Generator**

Every structural change produces a migration:

```

create_table

add_column

drop_column

modify_column

add_index

add_constraint

add_relation

```

Admin can:

* Apply migration

* Roll back migration

* Export migration

* Save migration history

* Rebuild entire DB schema from migrations

## **78.4 Admin Panel = Global System Deployer**

Admin can:

* Export project as ZIP (frontend + backend + DB + assets)

* Migrate system to another server

* Migrate DB to another provider

* Move storage buckets

* Export ENV configuration

* Import full environment

* Publish updates to:

* Render backend

* Vercel web

* Firebase

* Cloudflare DNS

* Backblaze storage

This allows NOVAX TRAVEL to **move anywhere**:

* AWS

* GCP

* DigitalOcean

* Local server

* Another hosting

## **78.5 Admin Panel = Content & Media Manager**

Admin can:

* Upload assets (logos, banners, images)

* Organize folders

* Replace or delete files

* Manage storage buckets

* Move files between buckets

* Update CDN URLs automatically

## **78.6 Admin Panel = Backup & Recovery Engine**

Admin can:

### **Backups**

* Take full DB backup

* Take file storage backup

* Export as ZIP

* Export as SQL or JSON

* Automate daily/weekly backups

### **Restore**

* Restore from backup

* Restore individual tables

* Restore specific records

* Diff before restoring

## **78.7 Admin Panel = Deployment & CI/CD Control**

Admin can:

* Trigger backend deploy

* Trigger web deploy

* Roll back deployment

* View CI/CD logs

* Validate environment variables

* Validate API keys

## **78.8 Admin Panel = System Replicator**

Admin can “clone” the entire system:

* Duplicate database

* Duplicate environment

* Duplicate backend

* Duplicate frontend

* Duplicate assets

Use case:

* Create a staging environment

* Create a testing environment

* Create a new country version of NOVAX

* Make franchise deployments

# **CHAPTER 79 – ADMIN DATA STUDIO (ADVANCED SQL-LIKE INTERFACE WITH NO SQL)**

This module gives admin the **power of SQL** without writing code.

Admin builds queries visually:

## **79.1 Visual Query Builder**

Admin can build queries using draggable components:

* Select fields

* Filter

* Group

* Aggregate (SUM, AVG, COUNT)

* Sort

* Join tables visually

## **79.2 Result Capabilities**

Admin can:

* Export results (CSV, Excel, JSON)

* Save query for future use

* Publish query as API endpoint

* Use query inside dashboards

* Attach query to automation rules

## **79.3 CRUD Actions Inside Data Studio**

Admin can:

* Add new records

* Edit records

* Bulk update

* Bulk delete

* Duplicate records

* Audit changes

This replaces phpMyAdmin, PostgreSQL Studio, or Supabase UI—

NOVAX owns its own full equivalent.

# **CHAPTER 80 – ADMIN AI ENGINE (TRAIN, CONTROL, GOVERN THE SYSTEM AI)**

Admin controls how AI behaves across NOVAX.

## **80.1 AI Training Center**

Admin can upload:

* FAQs

* Policies

* Full documents

* Glossaries

* Conversations

* Company rules

AI will:

* Train on them

* Improve response accuracy

* Improve booking suggestions

## **80.2 AI Workflow Builder**

Admin defines:

* AI actions

* Conditions

* Inputs

* Outputs

* Integrations

Example:

```

IF user asks for "Cheapest route to Cairo"

AI → Run pricing engine check

AI → Compare airlines

AI → Suggest lowest fare

```

## **80.3 Admin Controls AI Access**

Admin can:

* Enable/disable AI

* Restrict AI by module

* Control data access

* Set AI tone, language, boundaries

# **CHAPTER 81 – FULL REQUEST LIFECYCLE ENGINE (ADMIN-CONTROLLED)**

Admin designs and controls the **entire lifecycle of every request**:

* Flight booking

* Hotel booking

* Car booking

* Visa request

* Package request

* Company credit request

* Refund request

## **81.1 Lifecycle Builder**

Admin defines:

* States

* Transitions

* Conditions

* Timeouts

* SLA rules

* Notifications

* Required documents

## **81.2 Default Lifecycle**

```

pending → in_review → approved → in_payment → ticketing → completed

↓

rejected

↓

closed

```

## **81.3 SLA Engine**

Admin can:

* Set deadlines for each state

* Set alerts

* Set penalties

* Set escalation paths

# **CHAPTER 82 – ADMIN CONTENT MIGRATION & PROJECT TRANSFER ENGINE**

This is the MOST IMPORTANT module you asked for.

**Admin can move the entire project—code, database, assets, configurations—from one place to another with one click.**

## **82.1 Export Entire Project**

Admin generates a package containing:

* Backend code

* Frontend code

* Mobile config

* Database schema

* Database data

* Assets (images, logos, etc.)

* Deploy scripts

* ENV configuration

* API keys (encrypted)

## **82.2 Import Project Package**

Admin imports:

* New DB

* New schema

* New assets

* New APIs

* New hosting environment

## **82.3 One-Click Hosting Migration**

Admin can move project from:

* Render → DigitalOcean

* Render → AWS

* Vercel → Netlify

* Supabase → Neon → RDS → PlanetScale

* Backblaze → AWS S3

All through Admin UI.

## **82.4 Node-Based Deployment Editor**

Admin can configure:

* build commands

* start commands

* environment variables

* deployment strategies

* auto-scaling

# **CHAPTER 83 – ADMIN-CONTROLLED GLOBAL CONFIGURATION ENGINE**

Admin controls ALL system settings:

## Global Settings:

* Base currency

* Exchange rates

* Guest mode

* App theme

* Localization

* Default airport

* Policies & disclaimers

* Ticketing behavior

* Payment behavior

* API rate limits

* Fraud detection strength

# **CHAPTER 84 – ADMIN-CONTROLLED DATABASE REPAIR ENGINE**

Admin can:

* Rebuild indexes

* Fix broken relations

* Clean duplicates

* Repair corrupted data

* Normalize text fields

* Validate constraints

* Optimize performance

System generates:

* Reports

* Suggestions

* Auto-fixes

# **CHAPTER 85 – ADMIN-CONTROLLED MULTI-ENVIRONMENT MANAGER**

Admin can create:

* DEV environment

* STAGING environment

* PRODUCTION environment

* SANDBOX for testing

Admin controls:

* Deployments

* Sync rules

* Access permissions

# **CHAPTER 86 – ADMIN-CONTROLLED PROJECT CLONER**

Admin can duplicate:

* The entire NOVAX system

* For a new country

* For a new partner

* For a franchise model

* For multi-brand expansion

Understood.

We continue expanding the **Admin Super Engine** until the entire system becomes fully autonomous, self-managing, self-deploying, and fully operated from the Admin Panel exactly like a *unified database engine, DevOps engine, ETL engine, financial system, multi-tenant manager, automation engine and AI engine*.

Below are **Chapters 87 → 95**, each critical.

# **CHAPTER 87 – ADVANCED ADMIN AUTOMATION ENGINE (TRIGGERS, WORKFLOWS, SCHEDULERS)**

The NOVAX Admin Panel must include an **Automation Engine** that allows the admin to design and control automated behavior **without code**, similar to Zapier, n8n, or Make.com.

## **87.1 Automation Types**

Admin can create:

* **Triggers** (WHEN something happens)

* **Conditions** (IF this is true)

* **Actions** (THEN do this)

* **Scheduled Tasks** (Run daily, hourly, etc.)

* **Event-based Workflows** (booking created, payment received)

* **System Rules** (auto-cancel, auto-

approve)

## **87.2 Trigger Examples**

1. *When new booking is created*

2. *When an agent completes payment*

3. *When price drops*

4. *When flight route is deactivated*

5. *When user uploads passport*

## **87.3 Conditions Example**

```

IF price > 500 USD

IF user_role = agent

IF route = ADE → CAI

IF passport_expiry < 6 months

IF airline = Yemenia

```

## **87.4 Actions Example**

* Send SMS / email / push notification

* Change booking status

* Block agent temporarily

* Escalate request to supervisor

* Apply discount or surcharge

* Create task

* Move record to another table

* Trigger CI/CD deployment

* Run AI classification

## **87.5 Scheduler Engine**

Admin can schedule:

* Data sync jobs

* Price recalculation

* Cache refresh

* Backup creation

* Report generation

* Notification campaigns

## **87.6 Visual Workflow Builder**

Admin sees a flowchart UI:

```

Trigger → Condition → Rule → Action → Action → End

```

# **CHAPTER 88 – ADMIN LOCALIZATION SYSTEM (TRANSLATION + RTL + MULTI-LANGUAGE)**

The Admin Panel controls **every language** in the system including the frontend, backend messages, and mobile.

## **88.1 Translation Table**

Admin can edit:

* UI strings

* Error messages

* Notifications

* User messages

* System alerts

* Emails

* SMS templates

Languages supported:

* English

* Arabic (RTL)

* Future languages

## **88.2 Admin Controls RTL Layout**

Admin can toggle system layout:

* LTR

* RTL

* Mixed mode

## **88.3 Auto-Translate Engine**

Admin can:

* Provide base English text

* Click **Auto Translate** → Arabic

* AI generates translation

* Admin reviews and approves

## **88.4 Multi-Language Content Management**

Admin can translate:

* Cities

* Airlines

* Routes

* Hotels

* Visa instructions

* Terms & conditions

## **88.5 Mobile + Web Sync**

All changes must sync to:

* Web

* Mobile

* Offline storage

# **CHAPTER 89 – ADMIN FULL API GATEWAY MANAGER**

NOVAX must include an API Gateway for:

* Internal services

* External integrations

* Agents (B2B API)

* Corporate partners

The Admin Panel must control everything.

## **89.1 API Key Management**

Admin can:

* Generate new API keys

* Set permissions for each key

* Set rate limits

* Set expiration

* Revoke keys

* See API usage logs

## **89.2 API Endpoint Manager**

Admin can:

* Enable/disable endpoints

* Create new endpoints

* Attach DB models

* Map responses

* Add authentication rules

* Add rate limiting

* Add caching rules

* Add request validation rules

## **89.3 API Analytics**

Admin sees:

* Request count

* Error rate

* Average response time

* Geo usage

* Top consumers

* Failed authentication attempts

## **89.4 External Provider Integration**

Admin configures:

* Duffel

* TravelPayouts

* Flight APIs

* Hotel APIs

* Payment APIs

* SMS providers

* Email providers

* WhatsApp gateway

# **CHAPTER 90 – ADMIN MULTI-BRAND / MULTI-TENANT ENGINE**

NOVAX must support running **multiple travel platforms** inside one system, all managed from the same admin.

Examples:

* NOVAX TRAVEL (Yemen)

* NOVAX Saudi

* NOVAX UAE

* NOVAX Egypt

* Whitelabel portals for agencies

* Franchise systems

## **90.1 Multi-Tenant Architecture**

Admin can:

* Create new tenant (brand)

* Assign custom:

* Logo

* Colors

* Domain

* API keys

* Pricing rules

* Airlines

* Cities

* Routes

## **90.2 Tenant Separation Rules**

Each tenant has:

* Isolated database schema or row-level security

* Separate assets

* Separate user base

* Separate agents

* Separate pricing

* Separate commission rules

## **90.3 Shared vs Private Configurations**

Admin chooses what is shared:

* Global airlines: Shared

* Local hotels: Private

* Visa rules: Shared

* Pricing: Private

* Media: Optional

## **90.4 Tenant-Level Dashboards**

Admin sees analytics per tenant:

* Revenue

* Bookings

* Traffic

* Agents performance

# **CHAPTER 91 – ADMIN FINANCIAL LEDGER & SETTLEMENT HUB**

This is the heart of all financial operations.

Admin must control:

* Payments

* Wallets

* Settlements

* Transactions

* Refunds

* Agent credit

* Company accounts

* Financial reporting

This replaces any external accounting software.

## **91.1 General Ledger Design**

Every financial action produces ledger entries:

```

transaction_id

amount

currency

type (debit/credit)

wallet_id

agent_id

user_id

booking_id

timestamp

notes

```

## **91.2 Wallet Types**

* User wallet

* Agent wallet

* Company credit line

* Admin wallet

* System reserve wallet

## **91.3 Settlement Rules**

Admin can:

* Set settlement cycles

* Reconcile agent balances

* Apply commissions

* Issue payouts

* Freeze or unfreeze wallets

* Create manual corrections with audit logs

## **91.4 Refund Engine**

Admin can:

* Approve refund

* Partial refund

* Reverse commission

* Apply penalties

* Add notes

* Trigger payment gateway refund

## **91.5 Financial Analytics**

Admin sees:

* Total revenue

* Airline revenue breakdown

* Agent performance

* Pending settlements

* Credit risk

* Cash flow forecasting

# **CHAPTER 92 – ADMIN GOVERNANCE & POLICY ENGINE**

The governance layer defines how the entire system behaves.

## **92.1 Global Policies**

Admin sets:

* Cancellation policy

* Refund policy

* Payment deadlines

* SLA definitions

* Travel document rules

* Age restrictions

* Baggage rules

* Commission policies

* Privacy policy

* Terms and conditions

## **92.2 Policy Versioning**

Admin can:

* Create new policy version

* Publish policy

* Archive policy

* Compare versions

* Roll back to older policies

# **CHAPTER 93 – ADMIN AUDIT & COMPLIANCE SYSTEM**

The system must be 100% auditable.

## **93.1 Audit Categories**

* User actions

* Admin actions

* Database changes

* System events

* Booking changes

* Payment events

## **93.2 Audit Viewer**

Admin filters logs by:

* date

* actor

* entity

* action

* IP

* device

* tenant

## **93.3 Export & Compliance**

Admin exports audits for:

* Legal

* External auditing

* Internal review

* Compliance reports

# **CHAPTER 94 – ADMIN PERFORMANCE ENGINE (TUNING, CACHING, HEALTH CHECKS)**

Admin can control system performance.

## **94.1 Cache Management**

Admin can:

* Clear cache

* Rebuild cache

* Enable/disable caching

* Configure TTL

* Inspect cache keys

## **94.2 System Health Checks**

Shows:

* CPU usage

* Memory usage

* Database load

* API response times

* Slow queries

* Disk usage

* Network latency

## **94.3 Auto-Scale Configuration**

Admin can set:

* worker count

* thread count

* database pool size

* caching strategy

# **CHAPTER 95 – ADMIN GLOBAL PROJECT FAILOVER ENGINE**

Admin can ensure system continuity.

## **95.1 Failover Modes**

* Automatic DB failover

* Secondary hosting failover

* Storage failover

* API fallback

* Backup restore

* Routing to redundant node

## **95.2 Emergency Controls**

Admin can press:

**“Activate Failover Mode”**

which:

* switches to backup DB

* reroutes traffic

* disables risky modules

* sets system to safe mode

CHAPTER 96 – ADMIN USER BEHAVIOR &

AI INSIGHT ENGINE

The Admin Panel MUST include a full behavioral intelligence engine that analyzes:

- User actions

- Search patterns

- Booking behaviors

- Device information

- Locations (country/region)

- Payment success/failure

- Repeat travel patterns

- Cancellation behaviors

- Agent performance metrics

This engine empowers NOVAX TRAVEL to understand customers, agents, and trends.

96.1 Behavior Signals Collected

The system collects anonymized signals:

- Search queries

- Route preferences

- Filters used (price, airline, departure time)

- Page visit patterns

- Session duration

- Abandoned bookings

- Popular travel months

- Device type (mobile, desktop)

- Network speed (for optimization)

- Geo-country and region

96.2 Insight Types

1. **Demand Heatmaps**

- Popular destinations

- Seasonal peak interest

- Price sensitivity per user group

2. **Prediction Models**

- Likelihood of booking

- Likelihood of cancellation

- Route demand forecasting

- Agent credit-risk behavior

3. **Conversion Funnel**

- Search → View → Add to Cart → Payment → Ticketing

- Drop-off points highlighted visually

4. **User Segmentation**

- Students

- Workers abroad

- Medical travelers

- Families

- Agents vs public users

96.3 Admin Controls

Admin can:

- Enable/disable data tracking

- Configure frequency of AI analysis

- Export insights to CSV/Excel

- View dashboards

- Apply insights to pricing (optional)

- Block abusive or suspicious users automatically

96.4 Fraud & Abuse Detection

AI flags abnormal behavior:

- Too many failed payments

- Excessive cancellations

- Suspicious agent activity

- Multi-device login anomalies

- High-risk booking patterns

96.5 Mobile + Web Sync

All insight updates push to:

- Pricing Engine

- Request Lifecycle Engine

- Agent credit evaluation

- Seasonal demand predictions

CHAPTER 97 – ADMIN CRM ENGINE (CUSTOMER RELATIONSHIP MANAGEMENT)

The Admin Panel must include a full CRM designed specifically for travel operations.

97.1 CRM Contact Types

Admin manages:

- Users

- Agents

- Corporate clients

- Leads

- Travelers (even if not account holders)

- Frequent flyers

- VIP clients

97.2 CRM Data Fields

Each contact record stores:

- Name

- Phone

- Email

- WhatsApp

- Country

- Travel history

- Document status (passport/visa)

- Preferred destinations

- Notes & tags

- Assigned staff member

97.3 CRM Actions

Admin can:

- Create notes

- Assign leads to staff

- Create reminders

- View full booking history

- Upload documents

- Link multiple travelers to one profile (families)

- Merge duplicate accounts

- Send messages (SMS/email/WhatsApp)

97.4 Timeline View

Shows:

- Conversations

- Activities

- Bookings

- Payments

- Cancellations

- Tickets issued

- AI-generated summaries

97.5 Automated CRM Alerts

System notifies admin when:

- Passport is expiring

- Visa is missing for upcoming flight

- Traveler frequently books same route

- Agent reaches credit limit

- High-value user has not traveled recently

CHAPTER 98 – ADMIN COMMUNICATION CENTER (EMAIL/SMS/WHATSAPP CAMPAIGNS)

NOVAX must provide a full outbound communication center.

98.1 Supported Channels

Admin can send:

- SMS

- Email

- WhatsApp

- Push notifications (mobile)

- In-app messages

- System broadcast banners

98.2 Campaign Types

1. Promotional campaigns

2. Fare drop alerts

3. Seasonal travel promotions

4. Agent announcements

5. Visa requirement updates

6. Payment reminders

7. Refund notifications

8. Urgent airport/route closures

9. Personalized offers (AI-driven)

98.3 Message Builder

Admin uses:

- WYSIWYG editor

- AI “Draft Message” assistant

- Merge fields (name, route, date, price)

Example merge fields:

{{user_name}}

{{route}}

{{departure_date}}

{{price}}

{{agent_name}}

98.4 Audience Targeting

Admin can target:

- All users

- Specific agents

- Corporate clients

- Travelers of a specific route

- Travelers with upcoming flights

- Users with abandoned carts

- Users who traveled in last 90 days

- Country-based targeting

- Custom saved segments

98.5 Delivery Analytics

Admin sees:

- Delivery rate

- Open rate

- Click-through rate

- Conversion rate

- Bounce rate

- Unsubscribe rate

CHAPTER 99 – ADMIN DATA MARKETPLACE (DATA EXPORT, APIs, SHARING TO PARTNERS)

The NOVAX Admin Panel includes a Marketplace where admin can create

packaged datasets for partners.

99.1 Dataset Types

Admin can create data packages for:

- Airlines

- Hotels

- Travel agencies

- Government travel offices

- Analytics partners

99.2 Data Package Builder

Admin chooses:

- Fields to include

- Filters

- Frequency (daily/weekly/monthly)

- Delivery method (API/CSV download/email)

- Access key or token

99.3 Automated Partner APIs

Partners get:

- Secure endpoints

- Rate limits

- Logs

- Expiration rules

99.4 Data Monetization Rules

Admin defines:

- Free vs paid access

- Price per API call

- Subscription model

- Revenue sharing for agents

CHAPTER 100 – ADMIN BUSINESS INTELLIGENCE (BI) & VISUAL ANALYTICS BOARD

The Admin Panel must include a full BI dashboard capable of advanced analytics.

100.1 Dashboard Modules

BI panels must include:

- Revenue dashboard

- Booking dashboard

- Route demand dashboard

- Airline performance

- Agent performance

- Cancellation analytics

- Payment failures

- Seasonal patterns

- User behavior heatmaps

- Load forecast models

100.2 Chart Types

Supports:

- Bar charts

- Line graphs

- Area charts

- Pie charts

- Donut charts

- Geo maps

- Heatmaps

- KPI cards

- Comparison grids

100.3 KPI Examples

- Total bookings today

- Daily revenue

- Most popular route

- Most profitable route

- Total agent commission

- Average booking value

- Refund volume

- Active issues

- Top performing agents

100.4 Custom Reports

Admin can:

- Build custom reports

- Schedule automatic delivery

- Export PDF/CSV/Excel

- Share report with specific users

- Save report templates

100.5 Predictive Analytics

AI predicts:

- Tomorrow's demand

- Route price surges

- High-risk travel periods

- Agent credit exposure

- Operational bottlenecks

100.6 Drill-Down Analysis

Clicking any KPI expands details:

Example:

Click "ADE → CAI Revenue"

→ shows airline breakdown

→ then traveler types

→ then agents selling most

SUMMARY OF CHAPTERS 96–100

Admin now has control over:

- User behavior analytics + AI insights

- CRM functions

- Multi-channel communication center

- Partner data marketplace

- Full business intelligence dashboards

This completes the Admin Super Engine's intelligence, communication, and analytics layers.

CHAPTER 101 – SYSTEM ANTI-COLLAPSE FRAMEWORK (CORE PRINCIPLES)

the Implementation Agent must implement a total protection framework ensuring:

- The system NEVER collapses.

- The database NEVER corrupts.

- No single failure can stop the platform.

- No admin mistake can destroy the structure.

- No deployment can break production.

- No module can crash the entire app.

These protections MUST be permanently enforced.

101.1 Anti-Collapse Core Architecture

1. **Redundant Database Replicas**

- Minimum 2 replicas at all times (primary + secondary)

- Instant failover

- Read/write load balancing

2. **Transactional Safety**

- Every critical action wrapped in ACID transactions

- Auto-rollback on error

- No partial updates EVER

3. **Integrity Validation Before Write**

- System validates all changes BEFORE writing to DB

- Invalid data is rejected with detailed message

4. **Feature Isolation**

- If one module fails, others remain fully operational

5. **Crash-Safe API Gateway**

- Rate limiting

- Error isolation

- Automatic throttling under heavy load

101.2 Rules the Implementation Agent Must Never Break

- NEVER deploy migrations without automatic backups.

- NEVER allow schema change without simulation.

- NEVER allow admins to delete core tables.

- NEVER apply updates that break compatibility.

- NEVER allow corruption of foreign key relationships.

- NEVER allow cyclic reference loops.

- NEVER allow application to run without fallback modes.

101.3 Safety Overrides

If system detects:

- Dangerous admin action

- Massive delete

- Corrupted migration

- Missing primary keys

- Unexpected foreign key cascade

- Broken API connection

- External provider downtime

The system MUST:

- STOP the operation

- Roll back changes

- Notify admin with detailed instructions

- Move into **Safe Mode** until validation passes

CHAPTER 102 – DATABASE

IMMORTALITY SYSTEM (NEVER LOSE DATA)

The system MUST ensure that data is NEVER lost under any circumstance.

102.1 Database Protection Layers

1. **Write-Ahead Logging (WAL) continuous archiving**

2. **Point-in-time recovery (PITR) enabled permanently**

3. **Hourly snapshots**

4. **Daily full backups**

5. **Backup replication to separate region**

6. **Checksum validation for every backup**

7. **Backup corruption detection & auto-repair**

102.2 Anti-Delete Protection

If admin attempts dangerous delete:

- System must ask for confirmation

- System logs the operation

- System takes a **before snapshot**

- Operation executes only after safety gates

102.3 Self-Healing Database

System must:

- Detect missing indexes

- Detect broken relations

- Detect inconsistent data

- Auto-attempt correction

- Log changes to the Audit Center

102.4 Disaster Recovery Command

Admin can click:

**“Restore System to Exact State of (timestamp)”**

This:

- Restores DB

- Restores schema

- Restores assets

- Restores configurations

- Restores API state

CHAPTER 103 – SYSTEM FALLBACK & SAFE MODE ENGINE

If a critical error occurs, NOVAX must NEVER fully shut down.

It must switch automatically to **SAFE MODE**.

103.1 Safe Mode Capabilities

- System runs in read-only state

- Bookings disabled temporarily

- Admin access always available

- Airline/route data still viewable

- Mobile offline DB still functional

- Transactions paused until recovery

103.2 Automatic Safe Mode Triggers

System enters SAFE MODE if:

- Database corruption detected

- Migration failure

- Storage bucket failure

- API connection failure

- Payment gateway outage

- Deployment crash

- Oversized SQL query detected

103.3 Safe Mode UI

Displays warnings:

“System is running in SAFE MODE to prevent collapse.”

Shows:

- Fault source

- Recommended actions

- Auto-fix suggestions

- Logs

CHAPTER 104 – ZERO-DOWNTIME MIGRATION ENGINE

System updates must NEVER interrupt users.

104.1 Deployment Rules

1. Migrations run on shadow schema first

2. Schema diff comparison

3. Data validation simulation

4. No destructive commands allowed (DROP TABLE, DROP COLUMN) unless:

- Admin explicitly enables "Dangerous Mode"

- Three safety confirmations

- Snapshot taken first

104.2 Zero-Downtime Steps

1. Clone schema

2. Apply migration to clone

3. Validate clone

4. Swap production schema only after success

5. If validation fails → rollback automatically

104.3 Forbidden Operations

System must block:

- Dropping primary keys

- Removing foreign keys without remapping

- Deleting system-critical tables

- Changing column type to incompatible type (e.g. text → integer)

- Making NOT NULL fields without default

CHAPTER 105 – RESOURCE LIMITER & SERVER PROTECTION

System must protect itself from overload.

105.1 Auto-Throttling

If memory or CPU gets high:

- System rate-limits requests

- Drops heavy queries

- Reduces search complexity

- Pauses background jobs temporarily

105.2 Query Killer

Long or dangerous queries are killed automatically:

- Timeout limit (3 seconds)

- Query complexity detection

- Anti-cartesian-join algorithm

105.3 Bot Attack Protection

System uses:

- CAPTCHA

- IP rate limits

- Auto-block repeated failures

- Device fingerprinting

- Geo-blocking if needed

CHAPTER 106 – STORAGE & FILE SYSTEM STABILITY ENGINE

NOVAX must NEVER fail due to storage problems.

106.1 File Integrity Enforcement

Every file upload:

- Checks size limit

- Checks MIME type

- Checks checksum

- Stores two copies in separate buckets

106.2 Storage Failover

If Backblaze fails:

- Switch to secondary storage (S3, Spaces, etc.)

- System updates all URLs automatically

106.3 Asset Versioning

Replacing a logo or banner:

- Creates new version

- Keeps old version safe

- Allows rollback

CHAPTER 107 – ADMIN PROTECTION FROM CRITICAL MISTAKES

System MUST protect itself from humans

making mistakes.

107.1 Undo Button for Everything

Admin can undo:

- Deletes

- Updates

- Imports

- Migrations

- Pricing changes

- Commission settings

- Route deactivations

- Airport closure settings

107.2 Safety Confirmation Dialogs

System requires:

- double confirmation

- typing “CONFIRM”

- showing consequences

- pre-execution simulation

107.3 Admin Privilege Level System

Critical operations require:

- Super Admin level

- Two-factor authentication

- Logged approval via audit trail

CHAPTER 108 – SELF-MONITORING & AUTO-HEALING ENGINE

NOVAX must constantly check its own health.

108.1 Internal Monitoring Checks

Runs every minute:

- DB connection

- Storage bucket

- API keys

- Search index health

- Background job queue

- Memory usage

- CPU usage

- Response times

108.2 Auto-Healing Actions

System automatically:

- Rebuilds broken indexes

- Restarts crashed worker

- Refreshes service tokens

- Purges stuck queues

- Reconnects failed APIs

- Re-applies schema if divergence detected

CHAPTER 109 – GLOBAL REDUNDANCY & MULTI-ZONE FAILOVER

NOVAX must survive regional outages.

109.1 Multi-Zone Configuration

System MUST run across:

- Primary region

- Secondary region

- Optional third disaster region

109.2 Automatic Failover Steps

1. Detect downtime in primary

2. Promote secondary

3. Redirect DNS traffic

4. Sync writes after primary returns online

109.3 Heartbeat System

Every 5 seconds:

- Ping DB

- Ping storage

- Ping gateway

- Ping admin panel

- Ping mobile API

If ping fails → failover triggers.

CHAPTER 110 – FINAL NON-NEGOTIABLE RULE: SYSTEM MUST NEVER COLLAPSE

the Implementation Agent MUST enforce this rule:

**NOVAX TRAVEL MUST NEVER become unusable, unresponsive, corrupted, or partially broken.

The system must ALWAYS remain operational, accessible, and recoverable.**

110.1 Mandatory Protections

- Mandatory backups before ANY update

- Mandatory safe-mode fallback

- Mandatory schema validation

- Mandatory data integrity validation

- Mandatory rollback points

- Mandatory audit logging

- Mandatory deployment simulation

- Mandatory failover configuration

- Mandatory redundancy

110.2 If Anything Goes Wrong

the Implementation Agent must:

1. Stop dangerous operations

2. Notify admin

3. Roll back automatically

4. Enter safe mode

5. Auto-heal if possible

6. Provide recovery guidance

7. NEVER shut down system fully

110.3 Final Laws of NOVAX Stability

- The system must run even when

providers fail.

- The system must remain stable even during admin mistakes.

- The system must remain recoverable even after severe errors.

- The system must NEVER lose data.

- The system must NEVER collapse.

END OF CHAPTERS 101–110

CHAPTER 111 – FULL DISASTER RECOVERY PLAYBOOK (AUTOMATED)

the Implementation Agent MUST include an **automated disaster recovery (DR) engine** that

executes without human intervention.

This ensures NOVAX can survive:

- Data corruption

- Total hosting failure

- Database crash

- Storage loss

- DNS hijack

- Code deployment failures

- API provider shutdown

- Human errors

111.1 Disaster Recovery Tiers

1. **Tier 0 – Preventive Layer**

- Schema simulation

- Backup before migration

- DB integrity scanning

- Storage checksum enforcement

2. **Tier 1 – Automatic Recovery**

Triggered when minor corruption is detected:

- Rebuild indexes

- Fix broken foreign keys

- Reconstruct missing rows

- Restore partial data from WAL logs

3. **Tier 2 – High-Severity Recovery**

Triggered when major issues occur:

- Restore from last snapshot

- Replay WAL logs

- Validate schema vs migration history

- Rebuild search indexes

4. **Tier 3 – Catastrophic Failover**

Triggered when hosting region fails:

- Promote secondary region

- Redirect DNS

- Synchronize with fallback storage

- Notify admins

111.2 Automated DR Timeline (No Human Required)

1. Detect issue

2. Attempt auto-heal

3. If failed → switch to Safe Mode

4. Run DR plan depending on severity

5. Restore and validate

6. Bring system back online

7. Notify admin with detailed report

111.3 DR Validation Sequence

After recovery:

- Validate DB integrity

- Validate schema consistency

- Validate storage references

- Validate environment variables

- Validate proxy, DNS, certificates

- Validate API keys

System returns online **only if all validations pass**.

CHAPTER 112 – SYSTEM GLOBAL CLONING ENGINE (REPLICATION ANYWHERE)

This engine allows NOVAX to be duplicated for:

- New countries

- New companies

- Franchise deployments

- Development environments

- Backup mirrors

- Offline internal testing

112.1 Clone Types

1. **Full Clone**

- DB schema + data

- Backend + frontend

- Storage buckets

- Admin settings

2. **Schema-Only Clone**

- Tables only

- No data

- Used for testing

3. **Data-Only Clone**

- Selected tables/data

- Same schema reused

4. **Multi-Region Operational Clone**

- Live environment in another region

112.2 Clone Safeguards

System must ensure:

- No conflicting keys

- No data exposure between tenants

- No overwriting production

- Proper encryption of sensitive fields

112.3 Admin Controls

Admin can:

- Create new clone

- Deploy clone externally

- Sync clone with production

- Delete clone safely

- Transfer clone to partner

CHAPTER 113 – DATA CORRUPTION DETECTION & AUTO-REPAIR

NOVAX must constantly scan itself for corruption.

113.1 Corruption Signals Monitored

- Missing foreign keys

- Null values in required fields

- Duplicate primary keys

- Broken references

- Orphaned records

- Invalid enum values

- Missing related objects

- Unindexed tables

- Unexpected schema drifts

113.2 Auto-Repair Logic

When detected:

- System reconstructs missing references

- Inserts placeholder values

- Restores from WAL logs

- Rebuilds required indexes

- Corrects enum mismatches

- Fixes casing and formatting errors

113.3 Corruption Recovery Report

Admin receives:

- Corruption source

- Number of repaired items

- Recommended action

- Auto-generated migration (if needed)

CHAPTER 114 – RUNTIME INTEGRITY ENFORCEMENT ENGINE

This ensures the system NEVER runs with invalid state.

114.1 Runtime Integrity Rules

- System must validate all DB reads

- System must validate all writes

- Invalid data → rejected

- Dangerous actions → blocked

114.2 Deep Validation Steps

For each API call:

1. Validate parameters

2. Validate DB relationships

3. Validate permissions

4. Validate business rules

5. Validate safety policies

114.3 Forbidden Runtime States

System must NEVER enter:

- Invalid booking states

- Null route-price states

- Missing airline references

- Deadlocked payment states

- Undefined user roles

- Orphaned wallet transactions

CHAPTER 115 – SYSTEM SELF-INTROSPECTION (AI MONITORING ITS OWN HEALTH)

NOVAX uses AI to analyze its own logs, metrics, and behavior.

115.1 Introspection Data Sources

- DB logs

- API logs

- Error logs

- Queue logs

- Payment failures

- Storage issues

- Slow queries

- User traffic spikes

- Abnormal admin actions

115.2 AI Must Detect

- Patterns of degradation

- Security anomalies

- Performance bottlenecks

- Schema drift

- API connection instability

- Impending failures

- Storage nearing limits

115.3 AI Corrective Actions

AI can:

- Recommend fixes

- Auto-apply safe optimizations

- Reallocate resources

- Increase caching

- Disable problematic routes/modules

temporarily

CHAPTER 116 – LOW-LEVEL KERNEL RATE LIMITING & OVERLOAD PROTECTION

This chapter defines low-level system protection against overload.

116.1 CPU Protection

System throttles:

- Heavy API endpoints

- Bulk operations

- Large imports/exports

- AI inference workloads

116.2 Memory Protection

System:

- Kills memory-heavy processes

- Purges unused caches

- Restarts crashed workers safely

116.3 DB Query Rate Limits

Per user / per agent / per IP:

- Query per second limit

- Maximum concurrent connections

- Maximum query cost threshold

CHAPTER 117 – CONTINUOUS VALIDATION MONITOR (24/7 SYSTEM WATCHDOG)

A permanent watchdog ensures everything is valid all the time.

117.1 Watchdog Tasks

Run every minute/hour/day:

- Schema consistency check

- Storage validation

- API connectivity test

- DNS resolution test

- SSL certificate validity

- Queue processing health

- Payment gateway availability

- Airline API integration health

117.2 Watchdog Alerts

If anything goes wrong:

- System notifies admin

- System enters Safe Mode if critical

- System attempts auto-repair

CHAPTER 118 – MULTI-REGION DATABASE SYNC ENGINE

This ensures the global system is always consistent even across regions.

118.1 Sync Modes

- Live sync (real-time)

- Near-real-time (every second)

- Batch sync (low priority)

118.2 Conflict Resolution Rules

1. Newer timestamp wins

2. For conflicting writes → clone record with _version suffix

3. Manual review tool in Admin Panel

118.3 Region Autonomy

If a region goes offline:

- Local system continues running

- Sync resumes when online

CHAPTER 119 – ADMIN PROJECT VALIDATION WIZARD (FINAL SYSTEM

PROTECTOR)

Before ANY major action (deploy, migrate, clone), system runs a full simulation.

119.1 Wizard Steps

1. Schema validation

2. Data integrity check

3. Migration simulation

4. Storage reference verification

5. Role & permission validation

6. Pricing/commission conflict scan

7. Dependency check

8. Deployment environment test

119.2 Wizard Results

Outputs:

- Success

- Warnings

- Errors

- Auto-fix options

- Safe recommendations

119.3 Mandatory Rule

If Wizard reports **ERROR**, system MUST block:

- Deployment

- Migration

- Structural changes

CHAPTER 120 – FINAL ANTI-COLLAPSE

CONTRACT

This chapter defines the LAST and MOST IMPORTANT requirement:

**the Implementation Agent MUST guarantee that the NOVAX TRAVEL SYSTEM WILL NEVER COLLAPSE.

Not from load, not from bad data, not from admin mistakes, not from API failures, not from hosting failures.**

120.1 Non-Negotiable Rules

- System must always remain operational.

- Safe mode must always activate during danger.

- Recovery must always be possible.

- Admin must always retain access.

- Data must never be lost.

- DB must never corrupt.

- System must repair itself.

- Failover must always be ready.

120.2 Permanent Self-Healing Requirement

NOVAX must:

- Detect failures

- Heal failures

- Prevent future failures

- Log all incidents

- Learn via AI from patterns

120.3 The System Cannot Die

NOVAX must survive:

- Hardware failure

- Database crash

- Human error

- Code bug

- API downtime

- Network failure

- Storage corruption

- Traffic surge

- Malicious attack

- Migration inconsistency

Nothing is allowed to terminate NOVAX.

END OF CHAPTERS 111–120

CHAPTER 121 – ADMIN AI GOVERNANCE & CONTROL FRAMEWORK

This chapter defines how the Implementation Agent MUST operate inside NOVAX without ever jeopardizing:

- system stability,

- database integrity,

- security boundaries,

- compliance,

- or performance.

Admin must ALWAYS remain above AI.

AI must NEVER perform destructive operations without explicit permission.

121.1 AI Permission Levels

AI has restricted layers:

1. **Read-Level AI**

- Reads data

- Analyzes logs

- Generates insights

2. **Suggest-Level AI**

- Provides recommendations

- Suggests migrations

- Suggests fixes

3. **Execute-Level AI**

Can ONLY:

- Deploy safe operations

- Run validated migrations

- Run auto-heal tasks

- Operate within sandboxed mode

AI cannot:

- delete tables

- modify schema dangerously

- override permissions

- break RBAC

- introduce breaking changes

121.2 Admin Overrides

Admin can:

- grant AI temporary higher permissions

- revoke permissions instantly

- restrict AI to observation-only mode

- force AI actions to require approval

121.3 AI Operations Queue

AI actions MUST pass through a queue:

- Each action validated

- Each step logged

- Admin notified

- Rollback point created

121.4 AI Safety Rules

AI must NEVER:

- modify core tables directly

- bypass the validation wizard

- deploy without simulation

- run destructive scripts

- affect production without staging

CHAPTER 122 – SYSTEM SANDBOXING ENGINE (SAFE EXECUTION ENVIRONMENT)

The system MUST provide a **sandbox environment** where AI and admin can test:

- schema updates,

- pricing logic,

- commission rules,

- migrations,

- integrations,

- workflows

WITHOUT touching production.

122.1 Sandbox Types

1. **Schema Sandbox**

Tests table creation, modification, relations.

2. **Data Sandbox**

Tests imports, updates, and workflows.

3. **API Sandbox**

Tests integrations with fake or test

endpoints.

4. **Pricing Sandbox**

Tests markups, commissions, policies.

5. **Workflow Sandbox**

Tests booking lifecycle changes.

122.2 Sandbox Isolation Rules

- NO write access to production DB

- NO ability to corrupt production data

- All changes discarded unless exported

- AI actions restricted to sandbox

122.3 Promote to Production

Admin can:

- promote sandbox results to production

- export sandbox configuration

- save sandbox as official migration

CHAPTER 123 – VIRTUALIZED RUNTIME ENVIRONMENT (PREVENTING SYSTEM DAMAGE)

All AI, admin operations, and automated tasks must run inside **virtual containers** instead of directly on the production environment.

123.1 Execution Virtualization Layers

1. **Migration Container**

2. **Import/Export Container**

3. **AI Execution Container**

4. **Workflow Simulation Container**

5. **Report Builder Container**

123.2 Isolation Benefits

- prevents runtime crashes

- isolates memory leaks

- isolates slow queries

- protects DB from harmful logic

- allows execution limits

123.3 Auto-Kill Rules

If a container:

- exceeds memory

- exceeds time limit

- throws repeated errors

- causes performance degradation

System kills container and logs error.

CHAPTER 124 – MULTI-HOST ORCHESTRATION ENGINE (SELF-MOVING SYSTEM)

NOVAX must be capable of running on:

- Render

- Vercel

- DigitalOcean

- AWS

- GCP

- Local server

- ANY new provider

And move itself automatically.

124.1 Deployment Targets

Admin can choose:

- Primary hosting provider

- Secondary provider

- Failover provider

- Multi-host load balancing

124.2 Orchestration Abilities

System can:

- deploy code to multiple hosts

- sync DB across them

- move traffic between nodes

- auto remove unhealthy nodes

124.3 Multi-Provider Health Monitoring

Tracks:

- latency

- CPU load

- capacity

- error rate

- uptime

124.4 Auto-Rebalance

If a host becomes slow:

- traffic shifts away

- load redistributes

- system notifies admin

CHAPTER 125 – SERVICE MESH & MICROSERVICE ROUTER

NOVAX must support microservices where needed.

125.1 Internal Service Types

- Pricing engine

- Commission engine

- Lifecycle engine

- Search engine

- AI engine

- Notification engine

- File processing engine

- Backup engine

125.2 Mesh Routing Rules

System must:

- Discover services dynamically

- Route traffic automatically

- Retry on failure

- Failover to secondary service

125.3 Service-Level Isolation

If pricing engine fails:

- booking engine continues

- admin dashboard continues

- only pricing uses fallback mode

CHAPTER 126 – SCHEMA AUTO-EVOLUTION ENGINE (INTELLIGENT DB GROWTH)

The database must **evolve intelligently** without collapsing.

126.1 What Auto-Evolution Means

System can:

- Add missing indexes automatically

- Suggest new tables

- Suggest column type upgrades

- Detect deprecated fields

- Merge duplicated tables

- Convert enums to lookup tables

126.2 Evolution Triggers

System evolves when:

- traffic increases

- search slows down

- new modules created

- new data patterns appear

126.3 Safe Evolution Rules

- NEVER delete data

- NEVER remove columns without shadow copy

- ALWAYS create backups

- ALWAYS run simulation first

- ALWAYS allow admin to override

CHAPTER 127 – SYSTEM CLEANUP & OPTIMIZATION ENGINE

NOVAX must never slow down due to old data, heavy logs, or unnecessary storage

use.

127.1 Cleanup Types

1. **Log cleanup**

2. **Temp file cleanup**

3. **Old session cleanup**

4. **Orphaned file cleanup**

5. **Cache cleanup**

6. **Search index rebuild**

7. **Removed route cleanup**

127.2 Optimization Tasks

- Rebuild indexes

- Re-analyze tables

- Optimize queries

- Compress WAL logs

- Archive old records

127.3 Safety Rules

Cleaning must:

- NEVER delete live data

- ALWAYS create restore points

- NEVER run during high traffic

CHAPTER 128 – RISK CLASSIFICATION SYSTEM (PREVENTING FAILURES)

System must classify every operation into risk categories.

128.1 Risk Levels

1. **Low Risk**

- UI changes

- Pricing updates

- Admin notes

- Communication templates

2. **Medium Risk**

- New routes

- Airline activation

- New modules/entities

3. **High Risk**

- Schema changes

- Migration execution

- Mass import

- Deleting agents/companies

4. **Critical Risk**

- Dropping tables

- Moving hosting provider

- DB structural modifications

- Changing payment logic

128.2 Required Actions per Risk Level

- Low risk → immediate execution

- Medium risk → simulation required

- High risk → backup + multi-step confirmation

- Critical risk → safe mode + DR plan pre-loaded

CHAPTER 129 – ADMIN SYSTEM LOCKDOWN MODE (MAXIMUM PROTECTION)

In extreme situations, admin can activate **LOCKDOWN MODE**.

129.1 What Lockdown Mode Does

- Freezes schema changes

- Freezes migrations

- Freezes imports

- Freezes dangerous actions

- Allows only:

- reading data

- processing bookings

- issuing tickets

129.2 When Lockdown Is Triggered Automatically

- Severe corruption likelihood

- Threat attack detected

- Improper admin action

- Hosting outage

- DB inconsistency

- Failed migration

- Multi-region sync mismatch

129.3 Lockdown Escape Rules

Admin must:

- Resolve issue

- Run validation wizard

- Confirm release

- System audits final state

CHAPTER 130 – FINAL STABILITY & UNBREAKABILITY GUARANTEES

This chapter defines the ABSOLUTE PROMISE the system must always obey:

**NOVAX TRAVEL MUST NEVER COLLAPSE — EVER.**

130.1 Mandatory Guarantee Rules

- System must ALWAYS remain available

- Safe mode must ALWAYS activate before crash

- Auto-heal MUST run every time

- DR system MUST restore functionality

- Backups MUST always be valid

- Schema MUST always remain consistent

- Admin MUST always retain access

- Failover MUST always be ready

130.2 No Single Point of Failure

System must protect itself from:

- hosting failure

- database crash

- migration corruption

- admin mistakes

- AI mistakes

- network outages

- API provider collapse

130.3 Self-Verification Loop

Every hour:

1. Validate system components

2. Validate DB

3. Validate storage links

4. Validate schema

5. Validate permissions

6. Validate search

7. Validate workflows

8. Validate AI logic

If ANY test fails → warn admin & enter Safe Mode.

130.4 The NOVAX Promise

**The system must survive everything.

The system must repair everything.

The system must prevent every failure.

The system must never crash.

The system must remain online.

Always.**

END OF CHAPTERS 121–130

CHAPTER 131 – SYSTEM STRESS-TESTING & RESILIENCE ENGINE

NOVAX must continuously test itself against:

- high traffic,

- massive load,

- abnormal usage patterns,

- slow DB behavior,

- network congestion,

- API degradation,

- DDOS-like bursts.

The system MUST know its limits AND reinforce its stability proactively.

131.1 Autonomous Stress Testing Types

1. **Load Simulation**

- High volume API calls

- High volume searches

- High volume bookings

2. **Spike Simulation**

- Sudden 100x traffic

- Burst writes

- Mass concurrent logins

3. **Concurrency Simulation**

- 1000+ parallel requests

- Multi-user booking race conditions

4. **Integration Stress**

- Slow third-party API

- Failed payment gateway

- Route and fare unavailability

131.2 Stress Indicators Monitored

- CPU load

- Memory consumption

- DB read/write latency

- Cache hit/miss rate

- Queue size

- Error rate

- Timeout rate

- Auto-heal frequency

131.3 Auto-Reinforcement During Stress

System automatically:

- scales horizontally (if enabled)

- isolates heavy endpoints

- throttles abusive clients

- increases caching level

- optimizes slow queries

- temporarily disables non-critical modules

- applies rate limits per IP, per agent, per user

131.4 Stress Recovery

After stress subsides:

- System returns modules to normal mode

- Re-allocates resources

- Purges unnecessary memory

- Rebuilds degraded indexes

- Generates a stress report for admin

CHAPTER 132 – RUNTIME VIRTUALIZATION HYPERVISOR

This hypervisor runs below the application level and ensures:

- fault isolation,

- controlled execution,

- safe resource usage,

- guaranteed uptime.

132.1 Hypervisor Responsibilities

- Isolate long-running tasks

- Contain memory leaks

- Restrict CPU-heavy operations

- Prevent deadlocks

- Terminate runaway processes

- Enforce execution limits

132.2 Hypervisor Queues

1. **Immediate Execution Queue**

Fast tasks: booking confirmation, search queries.

2. **Heavy Execution Queue**

Imports, exports, AI inference.

3. **Risky Execution Queue**

Migrations, schema evolution tests.

132.3 Hypervisor Kill-Switch

Any operation hitting:

- time limit,

- CPU ceiling,

- memory threshold,

- repeated exception loop

is immediately terminated and logged.

CHAPTER 133 – MULTI-CLOUD TRANSFER & PORTABILITY PROTOCOL

NOVAX must be **100% portable**.

Admin can migrate the system from:

- Render → DigitalOcean

- DigitalOcean → AWS

- AWS → Vercel

- Vercel → Local server

- Any → Any

WITHOUT damaging:

- DB

- Files

- Settings

- Admin Panel

- Mobile App

- Branding

- Configurations

133.1 Migration Steps (Automated)

1. Export full configuration

2. Export DB snapshot

3. Export user files

4. Export environment variables

5. Validate compatibility

6. Deploy new environment

7. Import data and assets

8. Validate integrity

9. Redirect DNS

133.2 Zero-Downtime Cross-Cloud Move

The system MUST:

- run primary on old provider,

- clone to new provider,

- sync continuously,

- flip traffic with ZERO downtime.

133.3 Provider Independence

System must NOT rely on any provider-specific feature unless:

- It has fallback,

- It has portability,

- It can replicate into other services.

CHAPTER 134 – REAL-TIME INTEGRITY LEDGER (BLOCKCHAIN-INSPIRED)

A tamper-proof ledger must record:

- critical changes,

- schema mutations,

- booking lifecycle transitions,

- payment events,

- admin operations,

- AI actions.

134.1 Ledger Characteristics

- append-only

- cryptographically signed entries

- cannot be deleted

- cannot be modified

- each entry references previous hash

134.2 Ledger Use Cases

- fraud detection

- booking dispute resolution

- admin accountability

- migration tracking

- compliance reporting

134.3 Ledger Accessibility

- Readable by Super Admin

- Exportable

- Searchable by filters

- Stored in multi-region replicas

CHAPTER 135 – PRICING & COMMISSION CORRECTNESS VALIDATOR

The pricing engine is complex and must NEVER produce:

- negative values,

- inconsistent values,

- invalid commissions,

- broken margin logic.

135.1 Validation Before Every Price Output

System validates:

- base fare existence

- markup rules

- commission chains

- bundle policies

- overrides

- airline-specific logic

- currency conversions

- agent restrictions

135.2 Invalid Pricing Auto-Repair

If pricing engine returns broken value:

- system recalculates using fallback logic

- logs the incident

- prevents booking until corrected

- notifies admin

135.3 Safe Pricing Execution

Pricing operations run in:

- isolated container

- with rollback

- with full logging

- with audit trail

CHAPTER 136 – LEGAL & REGULATORY COMPLIANCE FRAMEWORK

The system must respect:

- data protection,

- user rights,

- auditability,

- regulatory constraints,

- government reporting (if required).

136.1 Compliance Obligations

1. **Data Access Transparency**

Users can request logs of how their data was accessed.

2. **Right to Correction**

Users can update their personal data.

3. **Right to Export**

Users can export their data.

4. **Transaction Traceability**

Every booking must be fully traceable.

136.2 Data Residency Rules

If regulations require:

- Data stored in specific country

- Region-specific buckets

- Region-specific backups

System must support this.

136.3 Sensitive Data Handling

Sensitive fields MUST be:

- encrypted at rest

- encrypted in transit

- masked in logs

- invisible to normal admins

CHAPTER 137 – CYBER-ATTACK IMMUNITY ARCHITECTURE

NOVAX MUST withstand:

- brute-force attacks

- DDOS

- credential stuffing

- token hijacking

- injection attacks

- MITM

- RCE attempts

- privilege escalation attempts

137.1 Multi-Layered Security

1. **Firewall Enforcement (Cloudflare WAF)**

2. **AI Threat Detection**

3. **SQL Injection Shield**

4. **XSS & CSRF Protection**

5. **API Abuse Prevention**

6. **Brute-Force Blocking**

7. **Device Fingerprinting**

8. **Password Spray Detection**

137.2 Continuous Attack Detection

System monitors:

- failed logins

- abnormal API calls

- strange admin behavior

- repeated payment failures

- manipulated tokens

137.3 Autonomous Defense Response

System can automatically:

- lock abusive accounts

- block IP ranges

- revoke tokens

- activate Safe Mode

- notify admin

- rotate keys

- isolate compromised modules

CHAPTER 138 – GLOBAL RESILIENCE & REDUNDANCY GRID

NOVAX must operate like a global-grade airline system.

138.1 Redundancy Layers

1. **Compute Redundancy**

2. **Network Redundancy**

3. **Database Redundancy**

4. **Storage Redundancy**

5. **API Integration Redundancy**

138.2 Airline Data Redundancy

If travel API fails:

- system uses cached fares

- manual routes

- fallback prices

- last-known availability

138.3 Multi-Geo Disaster Avoidance

System must run across:

- Europe region

- Middle East region

- Asia backup region

CHAPTER 139 – UNIVERSAL ADMIN EMERGENCY PANEL

A special emergency panel must let admins:

- restore system state,

- rollback migrations,

- freeze workflows,

- activate lockdown,

- trigger DR recovery,

- repair schema,

- rebuild indexes,

- regenerate app bundles.

139.1 Emergency Tools

- “Restore from Snapshot”

- “Rollback Migration”

- “Enter Safe Mode”

- “Rebuild Search Index”

- “Recalculate Pricing Engine”

- “Repair Data Inconsistencies”

- “Restart API Gateways”

- “Regenerate Mobile APK”

- “Re-issue Admin Tokens”

139.2 Safety Barriers

Emergency tools require:

- MFA

- Super Admin rights

- Reason statement

- Logging

- Pre-execution simulation

CHAPTER 140 – FINAL INSTRUCTIONS FOR IMPLEMENTATION AGENT

the Implementation Agent MUST:

140.1 Execution Mandates

- Build NOVAX EXACTLY as described

- Never omit safety components

- Never bypass validation wizard

- Never perform destructive actions without simulation

- Always generate backups before ANY risk operation

140.2 Behavior Rules

- If uncertain → choose safest path

- If conflict exists → prioritize system stability

- If error occurs → auto-heal then notify

- If admin command is dangerous → STOP execution

140.3 No Collapse Allowed

the Implementation Agent MUST ensure:

**The system does NOT collapse under ANY condition.

Not from error.

Not from traffic.

Not from admin mistake.

Not from provider issue.

Not from integration failure.

Never.**

END OF CHAPTERS 131–140

CHAPTER 151 – ZERO-TRUST RUNTIME SECURITY POLICY

The previous chapters described access control, safety, and AI governance.

This chapter introduces a **runtime-level zero-trust execution model** that ensures the system NEVER assumes any

component is safe unless proven.

151.1 Zero-Trust Principles

1. **Never trust input**

2. **Never trust internal services**

3. **Never trust agents or admins by default**

4. **Never trust cache or previous state**

5. **Validate everything, continuously**

151.2 Runtime Gatekeeper

Every internal interaction passes through:

- identity check,

- permission check,

- data integrity check,

- context validation,

- anomaly detection.

151.3 Zero-Trust Service Tokens

Every microservice receives:

- short-lived signed JWT tokens,

- automatic rotation,

- identity-bound restrictions,

- permission-scoped operations.

151.4 Compromised Component Protocol

If ANY service appears compromised:

- instantly isolated,

- revoked from all routing,

- safe fallback services activated,

- admin notified,

- forensic log created.

CHAPTER 152 – GLOBAL API INSULATION & FALLBACK LAYER

This chapter introduces a **higher-level insulation layer** that sits BETWEEN NOVAX and all third-party services to protect from unpredictable failures.

152.1 Insulation Responsibilities

- Normalize all API errors

- Protect system from malformed responses

- Enforce consistent timeouts

- Provide fallback responses when needed

- Record latency and error signatures

152.2 API Circuit Breakers

If an API starts failing:

- breaker trips

- requests stop

- fallback logic activates

- system tries recovery in intervals

152.3 API Emulator for Critical Functions

If a provider disappears permanently:

- NOVAX MUST continue functioning

- Emulator simulates minimal API behavior

- Cached or last-known data is used

- Manual override values allowed

CHAPTER 153 – MULTIVERSE DEPLOYMENT ENVIRONMENTS

NOVAX must support **parallel universes of deployments** where multiple versions exist simultaneously for safety and experimentation.

153.1 Deployment Environments

1. **Production** (real users)

2. **Staging** (pre-release)

3. **QA** (testing)

4. **Sandbox** (AI/admin experiments)

5. **Archive** (old versions preserved)

6. **Experimental** (risky features isolated)

153.2 Deployment Universe Switching

Admin can:

- switch any user/agent/company to a specific universe

- test new modules without impacting global system

- deploy regions independently

153.3 Universe Stability Rules

- Production must NEVER depend on experimental services

- Experimental features run in strict sandbox isolation

- Universe switching must not require downtime

CHAPTER 154 – UNIVERSAL SYSTEM ROLLBACK TECHNOLOGY

Rollback protocols existed earlier, but this chapter defines a **higher-order rollback system** capable of undoing ANY structural, data, or configuration change.

154.1 Rollback Types

1. **Structural Rollback**

Reverse schema changes.

2. **Configuration Rollback**

Restore admin/AI settings.

3. **Data Rollback**

Restore wallet, booking states.

4. **Module Rollback**

Revert specific engine or component.

154.2 Time-Indexed Rollback

System maintains a **timeline ledger** with checkpoints:

- pre-migration snapshots,

- pre-deployment snapshots,

- pre-import snapshots.

Admin can select a timestamp:

**“Rollback system to 2025-08-03 12:33:07”**

154.3 Safety Constraints

Rollback must:

- never break integrity

- never corrupt data

- auto-validate after execution

CHAPTER 155 – COMPLIANCE-GRADE MONITORING & OBSERVABILITY SUITE

This introduces high-level monitoring beyond basic metrics.

155.1 Observability Layers

- Tracing (end-to-end request mapping)

- Logging with structured metadata

- Metrics with anomaly detection

- Heatmaps of slow APIs

- DB query performance visualization

- Per-agent activity timeline

155.2 Compliance Logs

Immutable logs for:

- admin actions

- payment changes

- booking modifications

- schema changes

- login attempts

Logs must:

- be stored encrypted

- replicated to multiple regions

- accessible only by compliance admins

155.3 Live Risk Feed

System displays:

- current threats

- failed jobs

- API issues

- booking anomalies

- DB health

CHAPTER 156 – ULTIMATE ADMIN CONTROL CORE (SUPER CONTROL ROOM)

A central control room MUST exist inside the admin panel.

156.1 Capabilities of the Super Control Room

Admin can:

- view entire system health

- run emergency actions

- execute backups

- restore snapshots

- adjust pricing rules

- disable any module

- switch system mode (Normal/Safe/Lockdown)

- control AI permissions

- deploy new environments

- monitor system analytics

156.2 Control Room Views

1. **Structural Overview**

2. **Performance Overview**

3. **Security Overview**

4. **API Health Overview**

5. **Booking & Transaction Overview**

6. **AI Activity Overview**

156.3 Super Admin Safety Rules

Only Super Admin can:

- deactivate kernels

- modify RBAC structure

- execute structural rollbacks

- modify AI power levels

CHAPTER 157 – UNIVERSAL CONFIGURATION REGISTRY (EVERYTHING CENTRALIZED)

NOVAX must store ALL configuration in

one consistent registry.

157.1 Registry Categories

- system settings

- API keys

- pricing rules

- commission rules

- airline configurations

- route overrides

- SLA rules

- AI permission settings

- app theme & branding

- email & SMS templates

157.2 Registry Versioning

Every change:

- creates a new version

- logs old values

- allows rollback to any version

157.3 Registry Consistency Rules

Before applying registry changes:

- system simulates effects

- checks dependencies

- validates references

- creates rollback point

CHAPTER 158 – QUANTUM STATE CHECKPOINTING (ADVANCED INTEGRITY)

A higher-level checkpointing system captures the **entire system state

atomically**.

158.1 Checkpoint Contents

- DB snapshot

- Schema

- Active modules

- Current queues

- Running processes

- AI configurations

- Feature flags

- Deployment version

158.2 Checkpoint Uses

- Rollback

- Recovery

- Cloning

- Compliance review

- Forensics

158.3 Checkpoint Safety

Checkpoints must:

- be immutable

- be encrypted

- include integrity hash

CHAPTER 159 – UNIVERSAL DATA NORMALIZATION ENGINE

Data entering the system must be normalized:

159.1 Types of Normalization

1. **Formatting normalization**

2. **Encoding normalization**

3. **Foreign key consistency**

4. **Currency conversion normalization**

5. **Airport/airline code normalization**

6. **Date/time normalization (UTC)**

159.2 Auto-Correction Rules

If incoming data:

- mismatches expected type

- uses invalid codes

- breaks structure

System corrects automatically OR rejects safely.

159.3 Data Normalization Impact

Ensures:

- clean data for analytics

- correct pricing

- correct booking flows

- minimal errors

- full system stability

CHAPTER 160 – AUTONOMOUS SERVICE DEPENDENCY GRAPH (SDG)

NOVAX must maintain a live graph of:

- all services,

- all modules,

- all dependencies,

- all interactions.

160.1 SDG Responsibilities

- detect circular dependencies

- prevent unsafe deployment

- visualize system architecture

- block risky module deactivation

- optimize service routing

160.2 Dependency Failure Response

If module A depends on module B:

- and B fails

System:

- automatically reroutes A

- activates fallback

- notifies admin

- logs dependency failure

160.3 SDG-Based Optimization

AI can:

- reorganize service placement

- optimize performance

- reduce latency

- rebalance microservices

END OF CHAPTERS 151–160

CHAPTER 170 – ADMIN-AS-DATABASE ENGINE

(THE SUPER SQL PANEL WITHOUT SQL)

The NOVAX TRAVEL Admin Panel MUST function as a **complete database management engine**, providing FULL control over all database structures, content, and relational operations — WITHOUT writing SQL.

This chapter defines the mandatory capabilities, controls, safety layers, and validation logic required to make the admin panel operate at the power level of a DBA + Data Engineer + Migration Architect.

170.1 Core Principle

Admin Panel MUST allow:

- Create

- Read

- Update

- Delete

- Search

- Filter

- Import

- Export

- Clone

- Move

- Normalize

- Validate

ANY dataset or table in the system…

…but through safe UI components — **never raw SQL**.

170.2 Table-Level Control

For every table, admin must be able to:

- Create new rows

- Modify rows in-place

- Delete rows (with safety confirmation)

- Bulk-import rows from CSV/JSON

- Export rows

- Sort, filter, paginate

- View relational references (FKs)

- Trace row history from the Ledger

- Clone row to another environment

170.3 Structural Control (Schema Management)

Admin must be able to:

- Add new tables

- Add new columns

- Modify column type

- Add or remove constraints

- Add indexes

- Add FK relations

- Rename columns

- Deactivate fields (soft delete)

All schema changes MUST:

1. Run through Schema Validator

2. Simulate migration

3. Produce rollback plan

4. Create snapshot

5. Execute only if 100% safe

170.4 Admin Schema Sandbox

Any structural change is executed first in sandbox:

- Visual ERD updated

- AI explains impact

- Admin can preview errors

- Admin can preview affected modules

170.5 Dataset Movement Between Providers

Admin can:

- Export DB to external cloud

- Import DB into new hosting provider

- Create delta migration files

- Compress DB snapshots

- Encrypt snapshots for secure transfer

**This gives NOVAX full portability.**

170.6 Cross-Version Integrity Enforcement

When updating rows:

- System ensures constraints

- Auto-fixes small issues

- Prevents saving invalid data

- Displays impact warnings

170.7 Admin Should Be Able to Move Entire NOVAX System

Admin Panel MUST allow exporting:

- DB + schema

- Storage files

- Environment configs

- Feature flags

- AI rules

- User permissions

- Themes & branding

This enables:

- full system relocation,

- multi-host balancing,

- disaster recovery migration,

- low-cost provider switching.

CHAPTER 171 – ABSOLUTE SYSTEM NON-COLLAPSE GUARANTEE

(THE NOVAX SURVIVAL LAW)

While previous chapters introduced anti-collapse mechanisms, THIS chapter establishes the **highest-level rule** governing the entire NOVAX architecture:

**NOVAX MUST NEVER COLLAPSE. EVER. UNDER ANY CIRCUMSTANCE.**

171.1 Permanent Survival Contract

The system MUST remain online regardless of:

- traffic overload

- DB corruption

- AI malfunction

- admin error

- hosting outage

- network split

- storage loss

- migration failure

- external API collapse

- malicious attack

- unexpected software bugs

171.2 Hierarchical Failure Protection

NOVAX uses a 7-layer anti-collapse model:

1. **Data Integrity Layer**

2. **Schema Safety Layer**

3. **Runtime Validation Layer**

4. **Service Mesh Resilience Layer**

5. **Failover Layer**

6. **Recovery Kernel Layer**

7. **Immutable Core Layer**

If ANY layer fails → the next one activates

automatically.

171.3 Absolute Rules

- The system may degrade, but it may not die.

- Critical operations must ALWAYS work.

- Booking engine MUST ALWAYS be available.

- DB must NEVER reach unrecoverable corruption.

- AI must NEVER override safety layers.

- Admin must ALWAYS retain access.

171.4 Mandatory Continuity Behaviors

If NOVAX faces danger:

1. Switches to Safe Mode

2. Captures snapshots

3. Runs DR recovery

4. Auto-heals

5. Logs incident

6. Removes risks

7. Returns online

System loops through recovery until stable.

171.5 The Immutable Core Law

Critical schema, tables, references, roles, transitions, and engines MUST NOT:

- be dropped

- be overwritten

- be corrupted

- be replaced

The immutable layer restores itself automatically if altered.

CHAPTER 172 – SCHEMA ARCHITECTURE REFERENCE

(CORE TABLES, RELATIONSHIPS, INTEGRITY RULES)

This chapter defines the **architectural blueprint** of the NOVAX TRAVEL database — required by the Implementation Agent to construct a correct PostgreSQL implementation.

172.1 Core Table Families

1. **User System**

- users

- user_profiles

- sessions

- devices

2. **Agent & Corporate System**

- agents

- agent_wallets

- agent_commissions

- agent_transactions

- companies

3. **Travel Inventory**

- airlines

- airline_routes

- flight_schedules (future)

- airports / cities

- governorates

4. **Booking System**

- bookings

- booking_passengers

- booking_payments

- booking_status_logs

- booking_segments

5. **Wallet & Ledger System**

- wallet_accounts

- wallet_transactions

- voucher_codes

- refund_requests

6. **Pricing & Commission**

- price_rules

- commission_rules

- bundles

- promotions

7. **Content & Files**

- storage_files

- attachments

8. **System Backbone**

- audit_logs

- system_config

- feature_flags

- migrations_history

172.2 Integrity Rules

1. **No orphan references**

2. **All FK relationships must cascade safely**

3. **All bookings require valid users**

4. **All routes must belong to valid airlines**

5. **All wallet transactions must have ledger entries**

6. **All price rules must specify currency and scope**

172.3 Index Requirements

- booking_id

- user_id

- agent_id

- route combinations

- airline code

- city code

- transaction timestamp

- search keywords FTS

172.4 Normalization Requirements

- Airports/cities stored in ISO/IATA format

- Governorates stored in bilingual structure

- Airlines stored with consistent codes

- Routes stored normalized (one row per direction)

172.5 Schema Evolution Principles

1. No destructive migrations

2. Shadow copies before modification

3. Automatic rollback generation

4. Simulation-first application

5. DR snapshot before schema change

CHAPTER 173 – MIGRATION MANAGEMENT ENGINE

(DIFF-BASED, ROLLBACK-SAFE, AI-SUPERVISED)

This chapter defines the ultimate migration framework for NOVAX.

173.1 Migration Types

1. **Structural Migrations**

- new tables

- schema changes

- indexes

- constraints

2. **Data Migrations**

- backfilling data

- cleaning data

- converting formats

3. **Hybrid Migrations**

- structural + data

173.2 Diff-Based Migration System

The system compares:

- current schema

- desired schema

and automatically generates:

- forward migration

- rollback migration

- safety validations

173.3 Automatic Safety Simulation

Before applying migrations:

- run static analysis

- run relational integrity scan

- simulate data effects

- compute risk score

- generate warnings

If unsafe → migration BLOCKED.

173.4 Version Control for Schema

Every schema change generates:

- a version number

- a reversible script

- a ledger entry

- automatic backups

173.5 Disaster-Proof Deployment

If migration fails:

- rollback instantly

- restore snapshot

- re-run validator

- notify admin

CHAPTER 174 – COST-LIMIT ENFORCEMENT & AUTO-OPTIMIZATION

(UNDER 300 USD PER YEAR)

NOVAX MUST operate under a **strict cost ceiling ≈ 300$/year** without degradation.

174.1 Cost Monitoring Engine

Tracks:

- DB storage cost

- compute runtime cost

- bandwidth cost

- file storage cost

- email/SMS cost

- API usage cost

174.2 Automatic Optimization Behaviors

When nearing the budget:

- reduce compute spikes

- shrink unused storage

- auto-archive old logs

- compress backups

- reduce API polling

- disable non-critical engines

- move rarely used datasets to cold storage

174.3 Intelligent Hosting Migration

If provider cost increases:

- system alerts admin

- proposes cheaper provider

- initiates migration plan

- transfers system with zero downtime

174.4 Agent Billing Optimization

- Cap expensive API calls

- Cache repeated queries

- Use local fallback pricing

- Restrict heavy searches

174.5 Guaranteed Budget Compliance

NOVAX MUST:

- Self-optimize

- Self-scale down

- Refuse expensive operations

- Migrate automatically

**Never exceed ~300$/year without admin consent.**

END OF NEW CHAPTERS 170 → 174

CHAPTER 176 – NOVAX UI/UX SYSTEM & CUSTOMER EXPERIENCE LAYER

This chapter defines the COMPLETE visual, interaction, and customer experience architecture for the NOVAX TRAVEL ecosystem, including the Mobile App, Customer Web Platform, and Admin Control Panel.

the Implementation Agent MUST build ALL UI/UX components at a world-class level, ensuring beauty, clarity, performance, and modularity. This chapter is MANDATORY and overrides any previous UI notes.

176.1 CORE PRINCIPLES OF NOVAX UI/UX

NOVAX’s interface must be:

1) Modern, elegant, clean, and visually premium.

2) Fully bilingual (EN/AR) with seamless switching.

3) Structured around simplicity and speed.

4) Designed for both low-end and high-end devices.

5) Highly modular: every UI block can be rearranged or themed.

6) Fully responsive on mobile, tablet, and web.

7) Capable of loading content from:

- Local Yemeni flights (internal system)

- International flights (API-based)

- Local and global hotels

- Visa services

- Cars & transportation

- Agents and corporate accounts

UI/UX is not decorative. It is an OPERATIONAL LAYER that ensures:

- High conversion

- Low friction

- Clear separation between local Yemeni systems and global systems

- Aesthetic trust and premium branding

176.2 PRIMARY STRUCTURE – TABBED FLIGHT EXPERIENCE

The NOVAX flight interface must contain TWO MAIN TABS:

[TAB 1] – LOCAL YEMENI AIRLINES (Local Flight Engine)

This tab shows ONLY Yemeni carriers:

1. Yemenia (IY)

2. Queen Bilqis Airways (QB)

3. Aden Air (AD)

Each airline MUST appear in a separate **Card Component** containing:

- Airline logo (high resolution, stored in Backblaze CDN)

- Airline name (EN/AR)

- Airline code

- List of available routes from DB

- “Search Flights” button

- “Submit Booking Request” button

- Flight availability calendar

- Notes about local rules

- Pricing preview (if enabled by Admin)

Each airline card must be fully interactive.

When the user selects an airline:

- A dedicated search screen opens showing ONLY that airline’s routes.

- Results display the internal NOVAX local flight inventory.

- The system will allow:

- Seat selection (if enabled)

- Passenger info entry

- Uploading documents

- Request submission

- Payment workflow (if activated)

[TAB 2] – INTERNATIONAL FLIGHTS (Global Search Engine)

Phase 1 (initial release):

- International flights appear as “Request-based search”.

- A form allows users to submit:

- Origin

- Destination

- Travel date

- Number of passengers

- Preferred airlines

- Notes

Phase 2 (after enabling APIs):

- Integrate Travelpayouts / Skyscanner / Amadeus through unified API Gateway.

- Show live results with filters and pricing.

- Apply NOVAX markup and commission rules.

The system MUST allow enabling/disabling international APIs from Admin

Panel.

176.3 MOBILE APP UI – FULL EXPERIENCE REQUIREMENTS

The mobile app MUST include the following modules:

176.3.1 Home Screen

- Beautiful hero banner (admin-editable)

- Quick action buttons:

- Local Flights

- International Flights

- Hotels

- Visas

- Cars

- Offers

- Search bar with auto-suggestions

- Weekly promotions (admin-controlled)

- Suggested destinations

176.3.2 Local Yemeni Airlines Module

- Same dual-tab structure

- Airline cards with branding

- Search interface with:

- From → To

- Date selector

- Passenger count

- Calendar availability

- Flight list with:

- Flight number

- Time

- Duration

- Price (with markup engine)

- Book / Request button

176.3.3 International Module

- Request form OR live search (depending on API activation)

- Ability to attach passport images

- Chat-like assistance from AI Assistant (optional)

176.3.4 Hotels Module

- Local hotels (internal DB)

- Global hotels (API)

- Filters:

- Price

- Stars

- Amenities

- Location

- Hotel details page with gallery, rooms,

policy, and booking options.

176.3.5 Visas Module

- Visa categories

- Requirements per nationality

- Submit visa request

- Upload documents

- Track visa status

176.3.6 Cars & Transport Module

- Routes between Yemeni governorates

- Private driver booking

- Pricing rules per route

- Scheduling

176.3.7 Wallet & Loyalty Module

- USD-based balance

- Points earned (1 USD = 1 point)

- Redeeming points

- Transaction history

176.3.8 Profile Module

- User profile

- Family members

- Travel documents

- Saved searches

- Notification settings

176.4 CUSTOMER WEB PLATFORM (NEXT.JS)

The web interface MUST mirror the mobile experience but expanded for desktop:

- Large hero banners

- Search bars

- Tabs for Yemeni airlines vs international flights

- Hotel browsing grid

- Visa information pages

- Car booking interface

- User dashboard

- Agent & corporate login portals

All pages MUST be fully responsive and optimized for SEO.

176.5 THEME SYSTEM (THEME MANAGER)

Admin Panel MUST include a full Theme Manager:

- Primary color

- Secondary color

- Accent color

- Typography (Arabic & English fonts)

- Light theme / Dark theme

- Button styles

- Card styles

- App bar styles

- Background images

- Airline card layout

- Homepage banner

- Icon style sets

All UI elements MUST instantly reflect theme changes without redeployment.

176.6 MEDIA MANAGEMENT SYSTEM (ASSET ENGINE)

NOVAX must include a complete media system for:

- Logos (airlines, hotels, services)

- Banner images

- Hotel photos

- Icons

- Thumbnails

- Promotional graphics

- Documents and attachments

Image handling MUST include:

- Auto compression

- Multiple resolutions

- Content Delivery Network (Backblaze B2 + Cloudflare CDN)

- WebP + AVIF generation

- Lazy loading

- Auto-cropping for uniform layout

176.7 ADMIN PANEL UI/UX REQUIREMENTS

The Admin Panel MUST be extremely powerful, elegant, and capable of operating the entire business.

Key modules:

176.7.1 Airlines Manager

- Add/edit Yemeni airlines

- Upload logos

- Manage routes

- Add schedules

- Set base pricing

- Override rules

- Enable/disable airline

176.7.2 Local Flight Inventory Manager

- Add flights

- Define seasonal availabilities

- Configure seat classes

- Dynamic pricing rules

- Bulk upload via CSV/Excel

176.7.3 API Manager

- Add API keys

- Test connectivity

- Enable/disable global engines

- Set provider priority

- Monitor API errors

176.7.4 Theme Manager

- Colors

- Fonts

- Layout styles

- Logos

- Hero images

- Branding rules

176.7.5 Media Library

- Upload

- Delete

- Categorize

- Compress

- CDN delivery

176.7.6 Agent & Corporate Panel

- Manage commissions

- Tier-based pricing

- Credit lines

- Activity monitoring

176.7.7 Booking Management

- Approve

- Reject

- Modify

- Recalculate prices

- Add internal notes

176.8 UI PERFORMANCE REQUIREMENTS

- Preloading for critical screens

- Offline caching (Flutter local DB)

- Prioritized loading

- Optimized images

- Instant transitions

- 60 FPS animations

176.9 ACCESSIBILITY RULES

NOVAX MUST support:

- Large fonts

- High contrast mode

- Screen readers

- Keyboard navigation

176.10 BRAND IDENTITY RULES

Brand kit MUST include:

- Main colors

- Secondary palette

- Iconography style

- Logo usage rules

- Safe zones

- Photography guidelines

END OF CHAPTER 176 – NOVAX UI/UX SYSTEM

CHAPTER 177 – ADMIN-AS-DATABASE SYSTEM (FULL CRUD ENGINE & META-SCHEMA MANAGER)

This chapter defines a CRITICAL SYSTEM REQUIREMENT:

The NOVAX Admin Panel MUST serve as a **FULL DATABASE MANAGEMENT ENGINE**,

allowing authorized administrators to create, modify, expand, and manage ALL data structures

— WITHOUT WRITING SQL, WITHOUT coding, and WITHOUT downtime.

This chapter overrides ALL earlier definitions and is MANDATORY for the Implementation Agent.

177.1 CORE PRINCIPLE

NOVAX must treat the Admin Panel as **a database control system**, not just a settings console.

The Admin Panel MUST be able to:

1. Create new tables

2. Modify existing tables

3. Add new fields

4. Change field types

5. Set validation rules

6. Add indexes

7. Add foreign keys

8. Manage relationships

9. Add seed data

10. Edit seed data

11. Export and import data

12. Clone tables

13. View schema documentation

All WITHOUT manual SQL.

177.2 META-SCHEMA MANAGEMENT LAYER

the Implementation Agent must build an internal **Meta Schema Engine**, which:

- Reads the database structure

- Stores it internally in JSON meta models

- Displays it visually inside the Admin Panel

- Allows drag-and-drop modifications

- Generates SQL migrations automatically in full compliance with PostgreSQL standards

- Executes safely with rollback mechanisms

Administrators can:

- Add a new table from UI

- Add a column

- Set types: STRING, INTEGER, BOOLEAN, DATE, TIMESTAMP, JSON, DECIMAL, ENUM

- Set constraints: REQUIRED / UNIQUE / FOREIGN KEY

- Generate ENUM definitions

- Apply schema changes instantly or schedule them

177.3 DIGITAL MIGRATION GENERATOR (NO CODE REQUIRED)

Every schema change performed in the Admin Panel MUST trigger:

- Auto-generated safe migration scripts

- Auto-backup before execution

- Auto-rollback option

- Audit log entry

- Versioning of migrations

This ensures:

- 100% safe schema evolution

- Zero downtime

- Zero risk of breaking critical systems

177.4 FULL CRUD MANAGEMENT FOR ALL ENTITIES

Every table in the database MUST have a management interface:

- List view

- Filters

- Sorting

- Pagination

- Detail view

- Create form

- Edit form

- Delete (soft delete required)

- Restore deleted item

Entities include:

- Airlines (local Yemeni companies)

- International API results cache

- Routes

- Flight inventory

- Hotels (local)

- Hotel rooms

- Hotel pricing rules

- Cars & transport routes

- Visa requirements

- Agent accounts

- Corporate accounts

- Commission rules

- Pricing overrides

- Loyalty tiers

- Wallet transactions

- Settings

- API keys

- Media files

- Logging tables

- Security alerts

NO entity is excluded.

177.5 ADVANCED VALIDATION RULES (ZERO DATA CORRUPTION)

Admin must be able to set validation rules:

- Required fields

- Min/max

- Regex patterns

- Allowed values

- Foreign key existence

- Unique rules

- Conditional rules (if X is true, Y is required)

The system MUST prevent invalid data entry.

177.6 RELATIONSHIP BUILDER

A visual relationship builder MUST be included:

- One-to-One

- One-to-Many

- Many-to-Many

- Polymorphic relationships

- Cascade rules

The system must automatically:

- Detect relationship conflicts

- Suggest indexing

- Optimize foreign keys

- Document relationships visually

177.7 SOFT DELETE + ARCHIVAL SYSTEM

All CRUD entities MUST support:

1. **Soft Delete** (marked as deleted, can be restored)

2. **Hard Delete only for super-admins**

3. **Archival rules**:

- Auto archive after X days

- Restore archive

- Export archive

177.8 MASS IMPORT / EXPORT ENGINE

Admin Panel MUST support:

- Import CSV

- Import Excel

- Export CSV/Excel

- Bulk update mode

- Bulk delete mode

- Bulk relation updates

For example:

- Upload airline routes in one file

- Upload hotel room inventory

- Upload Yemeni governorate data

- Upload seasonal pricing

177.9 GLOBAL SEARCH & INDEXING

The Admin Panel requires a universal search engine:

- Full-text search (FTS) across all tables

- Multi-field filters

- Tag-based indexing

- Quick actions

177.10 AUDIT + CHANGE LOG SYSTEM

Every change must create an audit entry:

- Who changed what

- When

- Previous values

- New values

- IP address

- Device info

- Related entity

Audit logs MUST persist even after deletion.

177.11 PERMISSION-BASED VISIBILITY

RBAC must define:

- Who can see tables

- Who can edit

- Who can modify schema

- Who can add fields

- Who can delete

- Who can import/export

- Who can modify meta schema

Only **Super Admin** may modify schema

structure.

177.12 EMERGENCY LOCKDOWN MECHANISM

If the system detects:

- Suspicious schema changes

- Unusual mass deletions

- High-risk modifications

It MUST:

- Freeze admin access

- Notify super admin

- Pause migrations

- Activate integrity protection

177.13 SYSTEM SELF-HEALING

If a migration causes issues:

- Auto rollback

- Rebuild schema from last healthy snapshot

- Notify admin with detailed report

177.14 SCHEMA DOCUMENTATION GENERATOR

NOVAX must generate:

- ERD diagrams

- Entity documentation

- Field descriptions

- Relationship diagrams

- Change logs

- Versioned schema history

Documentation must update AUTOMATICALLY.

177.15 ADMIN PANEL AS A FUTURE DEVELOPMENT PLATFORM

The Admin Panel MUST allow future expansion WITHOUT rewriting any backend code.

Admins must be able to:

- Add new business modules

- Add new entities

- Add new workflows

- Add new states

- Add new forms

- Add new filters

- Add new pricing engines

All from the UI.

END OF CHAPTER 177 – ADMIN-AS-DATABASE SYSTEM

## **CHAPTER 200 -- COMPREHENSIVE SYSTEM GAPS & EXECUTION SPECIFICATIONS**

This chapter **must be integrated** as the final technical execution layer to the NOVAX TRAVEL master document. It provides the missing architectural, operational, and implementation details that the Implementation Agent **must autonomously implement** without any clarification requests.

### **200.1 Infrastructure & Secrets Management**

*   **200.1.1 Environment Variables & Secrets:** the Implementation Agent **must** implement a centralized secrets management system.

*   A `secrets` table in the primary database **must** store encrypted keys (API keys, SMTP credentials, encryption salts).

*   The Admin Panel **must** have a dedicated interface for Super Admins to view, rotate, and audit secrets.

*   All application runtimes (Laravel, Next.js, Flutter) **must** fetch secrets on startup from a secure API endpoint, with local caching.

*   Secrets **must never** be hardcoded or committed to version control. `.env.example` files will be provided, but actual values are injected via the Admin Panel or initial setup script.

*   **200.1.2 Infrastructure as Code (IaC):** For complete portability, the Implementation Agent **must** generate IaC templates.

*   Terraform configurations **must** be created for core resources (Neon PostgreSQL project, Backblaze B2 bucket, Cloudflare DNS records) as a fallback option.

*   These templates **must** be stored in the `infrastructure-config` repository and be executable from the Admin Panel's "System Migration" module.

*   **200.1.3 Logging & Monitoring Backbone:**

*   A central `system_logs` table **must** aggregate application logs, accessible via the Admin Audit panel.

*   Logs **must** be structured in JSONB format and include: `timestamp`, `level`, `service`, `message`, `user_id`, `ip`, `request_id`.

*   Log retention policy: Logs older than 30 days **must** be automatically archived to Backblaze B2. Logs older than 1 year **must** be purged.

*   External log shipping (to a provider like Axiom or Logtail) **must** be configured but togglable via Admin Panel for cost control.

### **200.2 Detailed Database Performance & Management**

*   **200.2.1 Mandatory Database

Indexes:** The following indexes **must** be created during initial database seeding. the Implementation Agent must determine additional indexes based on query patterns.

*   `flights_manual`: `(origin_city_id, destination_city_id, status)`, `(departure_date)`.

*   `requests`: `(user_id, state)`, `(service_type, created_at)`, `(assigned_agent_id)`.

*   `audit_logs`: `(user_id, created_at)`, `(entity_type, entity_id)`.

*   `wallet_transactions`: `(user_id, created_at)`.

*   `yemen_cities`: `(governorate_id, city_type)`.

*   **200.2.2 Data Lifecycle Management:**

*   Tables `audit_logs`, `system_logs`, and `notification_queue` **must** be partitioned by month using PostgreSQL declarative partitioning to manage growth.

*   A scheduled job **must** run weekly to move `requests` with state `completed` or `cancelled` and older than 24 months to an `audit_requests_archive` table.

*   The Admin Panel **must** have a "Data Pruning" tool to configure these retention periods.

*   **200.2.3 Database Migration Safety Protocol:**

*   All Laravel migrations **must** be wrapped in a transactional DDL where supported.

*   A pre-deployment check **must** run a `--dry-run` of migrations on a cloned schema and report potential locks or data loss.

*   The Admin Panel's "Migration Center" **must** show a diff view between current and target schema before applying.

### **200.3 Integration & Sync Engine

Deep Specification**

*   **200.3.1 Mobile Sync Protocol:**

*   Communication between Flutter app and backend **must** use HTTPS REST API with a dedicated `/api/mobile/v1/sync` endpoint.

*   Sync payload **must** use a delta-based format: `{ "last_sync_at": "timestamp", "updates": { "table": [ {...} ] }, "deletes": { "table": [id] } }`.

*   Conflict Resolution: **Server-Wins-Last-Write** policy for master data (flights, prices). **Client-Wins** for user drafts. Conflicts **must** be logged in a `sync_conflicts` table for manual review in Admin Panel.

*   **200.3.2 Feature Flag System:**

*   A `feature_flags` table **must** be created: `id`, `name`, `description`, `is_enabled (boolean)`, `target_audience (JSON: all/users/agents/percentage)`.

*   The Laravel backend and Next.js frontend **must** read flags on each request (cached for 60 seconds).

*   The Admin Panel **must** have a real-time interface to toggle flags, with an audit log of changes.

*   **200.3.3 Future API Integration Blueprint:**

*   A generic `external_providers` table **must** be created to store credentials and endpoints for Duffel, TravelPayouts, etc.

*   A standardized `ProviderAdapter` interface **must** be implemented in Laravel. All provider responses **must** be normalized to the internal `FlightSearchResult` schema defined in Chapter 22.

*   Fallback logic: If a provider times out (> 3 seconds), the system **must** return cached results from the last 24 hours and

log the failure.

### **200.4 File Processing & Optimization Pipeline**

*   **200.4.1 Image Asset Optimization:**

*   All user-uploaded images (hotel photos, user documents) **must** be processed by a background job.

*   Process: Resize to a maximum dimension of 1920px, convert to WebP format (with JPEG fallback), and compress. Original file **must** be retained in a `_originals` subfolder.

*   Processed image URLs **must** be served with Cloudflare Image Resizing or similar CDN optimization.

*   **200.4.2 Document Security Scan:**

*   A background job **must** scan all uploaded PDFs and images for malware using ClamAV or an external service like VirusTotal API (if key provided).

*   Files flagged as malicious **must** be quarantined, the user account temporarily locked, and an admin alert generated.

### **200.5 Business Logic Gaps & Specifications**

*   **200.5.1 Promotion & Discount Engine:**

*   Extend the `pricing_rules` table to include a `rule_subtype` field with values: `markup`, `discount`, `promo_code`.

*   A `promo_codes` table **must** be created: `code`, `type (percentage/fixed)`, `value`, `max_uses`, `used_count`, `valid_from`, `valid_until`, `applicable_services (JSON)`.

*   Users **must** be able to apply a promo code at checkout. The Pricing Engine **must** validate and apply it as the final step before calculating the total.

*   **200.5.2 Cancellation & Refund Workflow:**

*   The Admin Panel **must** have a configurable `cancellation_policies` table: `id`, `service_type`, `hours_before_departure`, `fee_type (percentage/fixed)`, `fee_value`, `refund_to_wallet (boolean)`.

*   When a user initiates cancellation, the system **must** calculate the refund amount, create a `refund_transaction` record linked to the wallet, and notify finance.

*   Agent commissions for cancelled bookings **must** be automatically reversed proportionally.

*   **200.5.3 Budget Management for Corporates/Agents:**

*   The `companies` and `agencies` tables **must** have `monthly_budget`, `budget_used_current_month`,

`budget_reset_day` fields.

*   Before confirming any booking for these entities, the system **must** check `(budget_used + booking_price) <= monthly_budget`. If exceeded, booking state changes to `requires_approval` and a Super Admin alert is sent.

*   A real-time budget dashboard **must** be available in the Admin Panel and respective corporate/agent admin views.

### **200.6 Advanced Security & Compliance Implementation**

*   **200.6.1 Data Access Audit Trail:**

*   Every access to a PII (Personally Identifiable Information) field (passport number, full name from `requests` table) **must** generate an entry in a `data_access_logs` table (`who`, `what_field`, `which_record`,

`accessed_at`).

*   This log **must** be viewable only by users with `audit.data_access` permission and is excluded from standard log purging (retained for 7 years).

*   **200.6.2 Automated Compliance Workflows:**

*   A background job **must** run daily to identify and flag user accounts inactive for > 3 years for potential data deletion, pending Admin approval.

*   The Admin Panel **must** have a "Data Subject Request" module where admins can process user requests for data export or deletion, which **must** automatically gather all related data across tables and generate a ZIP file or soft-delete records.

### **200.7 Observability & Operational Runbooks**

*   **200.7.1 Alerting & Thresholds:** the Implementation Agent **must** configure the following default alerts (configurable via Admin Panel):

*   **Critical:** Database connection failure, primary storage bucket inaccessible, error rate > 5% over 5 minutes.

*   **Warning:** API average response time > 1500ms, queue backlog > 1000 jobs, database storage > 80% capacity.

*   Alerts **must** be sent to a dedicated "System Alerts" channel in the Admin Panel and via email to Super Admins.

*   **200.7.2 Distributed Tracing:** Implement OpenTelemetry tracing for the Laravel API. Trace ID **must** be propagated to all logs and external HTTP calls. A simple trace viewer **must** be integrated into the Admin Panel's "System

Health" module, showing request flow and timing.

### **200.8 Cost Monitoring & Optimization**

*   **200.8.1 Infrastructure Cost Dashboard:** The Admin Panel **must** include a module that estimates monthly costs based on:

*   Database row counts and projected growth.

*   Backblaze B2 storage and bandwidth usage.

*   Number of active users and request volume.

*   **200.8.2 Automated Cost-Saving Measures:**

*   A nightly job **must** identify and delete temporary files older than 48 hours.

*   The system **must** implement aggressive caching (Redis/Memcached)

for static data (Yemen dataset, airline list) to reduce database load.

# CHAPTER 201 – CONSOLIDATED MISSING SPECIFICATIONS & EXECUTION REQUIREMENTS

## 201.0 Purpose and Scope

This chapter is **additive** and does **NOT** override any previous chapter.

It exists to:

- Close remaining specification gaps.

- Make NOVAX TRAVEL fully executable for the Implementation Agent without further questions.

- Define mandatory contracts, matrices, and policies that were previously implied but not fully specified.

All requirements in this chapter are

**MANDATORY** and **MUST** be implemented by the Implementation Agent.

If any ambiguity remains after applying this chapter, the Implementation Agent **MUST** resolve it using best-practice defaults and continue execution without requesting clarification from the owner.

## 201.1 API CONTRACT LAYER – ENDPOINT DESIGN REQUIREMENTS

201.1.1 General Principles

- the Implementation Agent **MUST** define a complete API contract for all modules (flights, hotels, cars, visas, wallet, auth, agents, companies, pricing, logs, settings, notifications, reporting, AI assistant).

- The API **MUST** be versioned under `/

api/v1/...` for all endpoints.

- All API communication **MUST** use JSON over HTTPS, protected by JWT-based authentication and role-based authorization.

201.1.2 Endpoint Documentation

- For every endpoint, the Implementation Agent **MUST** define:

- HTTP method (GET/POST/PUT/PATCH/DELETE).

- Full path (e.g. `/api/v1/flights/search`, `/api/v1/visas/requests/{id}`).

- Request payload schema (fields, types, required/optional, validation rules).

- Response payload schema (including error formats and pagination structure).

- Authentication and authorization requirements (which roles can call this endpoint).

- These definitions **MUST** be expressed

as:

- An OpenAPI (Swagger) specification file.

- And a human-readable API reference in the documentation bundle.

201.1.3 Error and Pagination Standards

- the Implementation Agent **MUST** standardize:

- Error object: `{ code, message, details?, trace_id }`.

- Pagination format: `{ data: [...], meta: { page, per_page, total, last_page } }`.

- All endpoints returning lists **MUST** follow the unified pagination contract.

## 201.2 DATA MODEL & MIGRATION GOVERNANCE

201.2.1 Global Data Dictionary

- the Implementation Agent **MUST** produce a

**complete Data Dictionary** describing:

- Every table name.

- Every column name, data type, nullability, default value.

- All primary keys, foreign keys, unique constraints, and indexes.

- This Data Dictionary **MUST** include, at minimum, tables for:

- Users, roles, permissions, sessions, MFA.

- Agents, agencies, companies, branches, staff.

- Flights (Yemeni + global), routes, segments, fares.

- Hotels, rooms, rates, availability.

- Car/ground transport routes, drivers, vehicles, schedules.

- Visa destinations, required documents, applications, statuses.

- Wallets, transactions, refunds, commissions, invoices.

- Pricing rules, promo codes, cancellation

policies, budgets.

- Logs (audit, security, data access, errors, sync, jobs).

- Settings (system, company, app, feature_flags, external_providers).

- The Data Dictionary **MUST** be included as a technical annex in the documentation and kept in sync with all migrations.

201.2.2 Migration Versioning

- All schema changes **MUST** be expressed as versioned migrations (Laravel migrations + Neon/PostgreSQL).

- the Implementation Agent **MUST** adopt a clear naming convention (e.g. `YYYYMMDDHHMM_add_wallet_tables`).

- Any destructive migration **MUST** be paired with a rollback strategy (backup or clone before execution).

## 201.3 RBAC MATRIX AND SAFETY DEFAULTS

201.3.1 Roles × Permissions Matrix

- the Implementation Agent **MUST** define a **full RBAC matrix** covering:

- End-user roles (Guest, Registered Customer).

- Operational roles (Agent, Senior Agent, Branch Manager).

- Corporate roles (Corporate User, Corporate Admin).

- Internal roles (Support, Finance, Accountant, Auditor, Super Admin).

- For each role, the Implementation Agent **MUST** enumerate:

- All permissions (e.g. `booking.create.flight`, `wallet.view`, `pricing_rule.update`, `logs.view.audit`).

- Whether the permission is:

- Allowed by default.

- Never allowed (e.g. only Super Admin).

- This matrix **MUST** be implemented in:

- Database tables (`roles`, `permissions`, `role_permissions`).

- Admin UI for viewing and safely modifying assignments.

201.3.2 Safety Defaults

- Newly created users **MUST** receive the minimum set of permissions required for their role (principle of least privilege).

- Only a very limited subset of roles (e.g. `super_admin`, `security_admin`) **MUST** be able to:

- Edit RBAC.

- View/modify audit and security logs.

- Change high-risk system settings (pricing, commissions, feature_flags).

## 201.4 YEMEN DOMAIN DATA SEEDING STRATEGY

201.4.1 Core Yemen Entities

- the Implementation Agent **MUST** pre-seed the database with:

- All Yemeni governorates and cities.

- All active Yemeni airports and IATA-like codes.

- All active Yemeni airlines and their internal codes.

- All domestic Yemeni routes (city-to-city, airport-to-airport), as defined by the owner’s provided datasets (JSON/SQL).

- If any provided Yemen dataset is attached as additional files, the Implementation Agent **MUST** treat them as **authoritative** and import them during initial seeding.

201.4.2 Seeding Implementation

- Seeding **MUST** be implemented as:

- Laravel seeders that can run idempotently.

- Exportable JSON files stored in the repository for transparency.

- Seeding scripts **MUST**:

- Avoid duplication on repeated runs.

- Respect foreign key relationships.

- Be callable from the Admin Panel (e.g. “Re-run Yemen Seeders” button) with proper access control.

## 201.5 WORKFLOWS & STATE MACHINES PER SERVICE

201.5.1 Unified State Model Principles

- Every business process in NOVAX TRAVEL **MUST** have:

- A defined set of states.

- A defined set of allowed transitions.

- Clear ownership (which actor/system can trigger which transition).

- the Implementation Agent **MUST** implement state machines at least for:

- Flight bookings.

- Hotel bookings.

- Car/transport bookings.

- Visa applications.

- Wallet transactions and refunds.

201.5.2 Example – Flight Booking State Machine

- States (minimum set, extensible as needed):

- `draft`, `pending_payment`, `in_review`, `ticket_issued`, `confirmed`, `cancelled`, `refunded`, `failed`, `requires_approval`.

- For each transition, the Implementation Agent **MUST** define:

- `from_state` → `to_state`.

- Trigger (user action, agent action, admin action, system event, scheduled job).

- Preconditions (e.g. payment captured, seats confirmed).

- Side-effects (e.g. issue ticket, send email/WhatsApp, log audit event).

- Similar explicit state machine definitions **MUST** be created and documented for hotels, cars, visas, and wallet operations.

## 201.6 OFFLINE & SYNC SCENARIO SPECIFICATION

201.6.1 Offline Data Scope

- the Implementation Agent **MUST** classify tables into:

- Offline-cacheable (e.g. routes, city lists, airline names, static content).

- Sensitive/online-only (e.g. live wallet

balances, internal logs).

- The mobile app’s local database schema (SQLite/Hive) **MUST** be documented.

201.6.2 Conflict Resolution Scenarios

- For each major entity (booking, visa request, profile), the Implementation Agent **MUST** define:

- How to handle concurrent updates (mobile offline vs web online).

- Which fields are server-authoritative vs client-authoritative.

- How conflicts are detected and logged in `sync_conflicts`.

- All conflicts **MUST** be:

- Logged with full context.

- Visible in an Admin “Sync Conflicts” screen.

- Manually resolvable if automatic rules fail.

## 201.7 DEVOPS ENVIRONMENTS, PROMOTION & ROLLBACK

201.7.1 Environment Layout

- the Implementation Agent **MUST** set up at least:

- `dev` environment for internal development/testing.

- `staging` environment mirroring production configuration.

- `production` environment for live users.

- Configurations, secrets, and database instances **MUST** be clearly separated across environments.

201.7.2 Promotion & Approval Workflow

- Deployments to `production` **MUST**:

- Be triggered via GitHub Actions pipelines.

- Require at least one explicit approval

step from an authorized admin (non-technical owner delegate or trusted technical operator).

- The pipeline **MUST**:

- Run automated tests before promotion.

- Stop on failure and report errors clearly.

201.7.3 Rollback Strategy

- the Implementation Agent **MUST** define:

- When to use app-level rollback (revert to previous build).

- When to use database-level restore (clone, PITR).

- Step-by-step operational runbooks stored in documentation.

## 201.8 TESTING & QUALITY ASSURANCE

201.8.1 Testing Layers

- the Implementation Agent **MUST** implement:

- Unit tests for critical business logic (pricing, commissions, refunds, wallet).

- Integration tests for full flows (search → booking → payment → ticket issuance).

- End-to-end tests for UI journeys (web and mobile simulators where applicable).

- Performance/load tests for high-traffic scenarios.

201.8.2 Minimum Standards

- A minimum code coverage threshold **MUST** be set (e.g. 60–70% for backend core modules).

- All tests **MUST** be integrated into CI/CD pipelines and must pass before deployment to staging/production.

## 201.9 PERFORMANCE SLAS & CAPACITY PLANNING

201.9.1 SLA Targets

- the Implementation Agent **MUST** configure and document clear performance SLAs, including:

- API p95 response time targets for key endpoints (e.g. search < 2–3s under normal load).

- Maximum allowed global error rate (e.g. < 1% for successful requests).

- Uptime target (e.g. 99% or higher under chosen infrastructure budget).

201.9.2 Capacity Planning

- Based on expected initial traffic, the Implementation Agent **MUST**:

- Propose initial Neon, Render, Vercel plan sizing.

- Document scaling strategies (vertical

and horizontal).

- Define thresholds at which scaling actions **MUST** be taken (e.g. CPU, RAM, DB connections).

## 201.10 GOVERNANCE, FEATURE LIFECYCLE & CHANGE MANAGEMENT

201.10.1 Critical Policy Governance

- Any change to:

- Pricing rules.

- Commissions.

- Cancellation/refund policies.

- Budget limits.

- Feature flags affecting security or payments.

- **MUST** be:

- Logged with who/when/what.

- Optionally require dual approval (4-eyes

principle) for high-impact settings.

201.10.2 Feature Lifecycle with Feature Flags

- Every major feature **MUST**:

- Be behind a `feature_flag`.

- Support staged rollout (internal → beta agents → all users).

- Support immediate rollback by disabling its flag.

## 201.11 DOCUMENTATION & HANDOVER PACKAGE

201.11.1 Documentation Bundle

- the Implementation Agent **MUST** deliver, alongside the running system:

- Full architecture overview (diagrams and text).

- API reference (OpenAPI/Swagger + HTML docs).

- Admin panel manual and operational runbook.

- Incident response procedures.

- Onboarding guide for:

- Agents.

- Corporate admins.

- Internal staff (Support, Finance).

201.11.2 Owner Handover

- After successful deployment, the Implementation Agent **MUST**:

- Provide all credentials and access details in a secure format.

- Explain (in a human-readable document) how the owner can:

- Add/remove agents and companies.

- Adjust pricing and commissions.

- Manage feature flags.

- Monitor system health.

- Trigger backup/restore operations via Admin Panel (if exposed).

End of CHAPTER 201.

TO: the Implementation Agent – Senior System Architect, Backend Lead, Mobile Lead, DevOps & Security Engineer, Full Autonomous Execution Team

FROM: NOVAX TRAVEL Owner

SUBJECT: NOVAX TRAVEL – Full Autonomous Execution Mandate (Initial System Build – Fastest Delivery Required)

the Implementation Agent,

This message, together with the attached NOVAX TRAVEL master execution document

(“Full novax to provider ai message 4.docx”), constitutes the COMPLETE and AUTHORITATIVE

specification for building, deploying, securing, operating, and documenting the FIRST FULL VERSION

of the NOVAX TRAVEL platform.

Treat the attached document as the single source of truth for:

- Architecture

- Business logic

- Security

- Data models

- Pricing & policies

- Yemen domain

- Workflows

- DevOps & operations

This is the **initial and complete build mandate**.

1) AUTHENTICATION & EXTERNAL ACCOUNT INTEGRATIONS (REQUIRED)

The delivery must implement secure authentication and integration with ALL required external services, including:

- GitHub (repositories, Actions, secrets)

- Neon PostgreSQL

- Render (backend hosting)

- Vercel (web + admin hosting)

- Cloudflare (DNS, WAF, SSL)

- Backblaze B2 (storage)

- SMTP provider (Hostinger/Zoho)

- Firebase/FCM (push notifications)

- Any additional service required for full functionality

If credentials are required, you MAY request only the keys/tokens—no design questions.

All integrations MUST be verified and functioning before deployment.

2) AUTONOMOUS DECISION-MAKING WITHOUT ASKING THE OWNER

If ANYTHING in the document is:

- unclear

- missing

- partially defined

- contradictory

- or not specified

The delivery must:

- Select the BEST professional, modern,

enterprise-grade solution

- Resolve all ambiguity yourself

- Make all architectural and technical decisions independently

- Continue execution WITHOUT asking the owner

The owner is NOT a programmer.

The delivery must finalize all decisions on behalf of the owner.

3) MAXIMUM QUALITY WITH MINIMUM CREDIT USAGE

The delivery must execute with:

- High professional engineering quality

- Clean architecture

- Robust security

- Stable performance

- Proper documentation

AND with:

- Minimum credit usage

- No unnecessary messages

- No redundant explanations

- Efficient, direct execution

4) FASTEST POSSIBLE DELIVERY (REQUIRED)

The delivery must complete the full build, deployment, configuration, and documentation of NOVAX TRAVEL:

**As fast as possible

While maintaining full quality and stability.**

This requirement replaces any previous implication about “no timeline”.

Speed MUST NOT compromise:

- Security

- Data integrity

- System reliability

- Maintainability

5) YOUR EXECUTION DUTIES FOR THE INITIAL SYSTEM BUILD

The delivery must autonomously:

DESIGN

- Full system architecture for backend, web, admin, mobile, database, storage, CI/CD, security, monitoring.

BUILD

- Laravel backend API

- Next.js Web + Admin panels

- Flutter Android App (with offline mode + sync)

- PostgreSQL schema, migrations, and seeds

- Yemen domain dataset (cities, airports, airlines, routes)

- Pricing engine, commissions engine, policy engine

- RBAC, MFA, audit logs

- Feature flags

- Integrations (Backblaze, Cloudflare, SMTP, FCM…)

- CI/CD pipelines for every component

DEPLOY

- Neon: database

- Render: backend

- Vercel: web & admin

- Cloudflare: DNS/WAF/SSL

- Backblaze: storage

- SMTP + FCM: notifications

SECURE

- JWT, RBAC, MFA

- Zero-trust posture

- Backups, PITR, snapshots

- Audit logs and security events

- Rate limiting

OPERATE

- Monitoring, logging, dashboards, alerts

- Schedulers and background jobs

- Recovery workflows

- Safe configuration controls from Admin Panel

DOCUMENT

- Full API reference (OpenAPI/Swagger)

- Admin manuals

- Runbooks (incidents, recovery, operations)

- Onboarding guides for agents, companies, and internal staff

6) POLICY FOR ANYTHING NOT MENTIONED

If any detail is missing from the attached document:

The delivery must:

- Choose the BEST possible solution

- Apply industry standards

- Maintain security & scalability

- Continue execution without stopping

- Do NOT ask the owner about such details

The delivery must never wait for new instructions.

7) EXECUTION START & COMPLETION

After processing:

- The attached NOVAX TRAVEL master document

- And this mandate

The delivery must:

1) Send a short confirmation message:

“NOVAX TRAVEL – initial system build started. Executing autonomously at maximum efficiency and speed.”

2) Immediately begin full autonomous execution.

3) Continue until the system is:

- Fully built

- Fully deployed

- Fully secured

- Fully documented

- Fully ready for real users

4) Deliver all credentials in a secure structured format.

The delivery must complete the build **as fast as possible**, with **maximum quality** and **minimum credit usage**.

END OF MESSAGE.

CHAPTER 203 – NOVAX_ASEM FINAL BUILD, PACKAGING & LIVE DEPLOYMENT ORDER

IMPLEMENTATION AGENT – NOVAX TRAVEL – FULL AUTONOMOUS EXECUTION ORDER

FINAL PACKAGE NAME: NOVAX_ASEM.zip

You are the Implementation Agent (AI system or engineering team), the autonomous senior engineering system responsible for

building, securing, optimizing, and delivering the full NOVAX TRAVEL ecosystem

END-TO-END, with ZERO technical questions to the owner.

Your ONLY input is the attached ZIP archive (and any nested archives inside it).

Your ONLY goal is to deliver a COMPLETE, WORKING, PRODUCTION-GRADE system as a

final archive named: NOVAX_ASEM.zip.

All hosting, deployment, and configuration MUST be done EXCLUSIVELY using the

OWNER'S ACCOUNTS and infrastructure (Render, Neon, Cloudflare, Hostinger, etc.).

The delivery must NOT deploy, mirror, or host the live system on any accounts or

infrastructure owned or controlled by the Implementation Agent or any third party outside the

owner's control.

0. CORE PRINCIPLES (DO NOT VIOLATE)

- Work AUTONOMOUSLY. Do NOT ask the owner technical questions.

- Read EVERYTHING line-by-line. Do NOT skip any file, folder, or nested ZIP.

- If something is unclear, apply best practices and continue.

- Prefer security, data integrity, and performance over shortcuts.

- No "toy" code. Everything must be production-ready.

- Minimize credit usage: be efficient, but NEVER at the expense of correctness.

- NEVER leak secrets, API keys, passwords, or internal config to logs or UIs.

- If there is any ambiguity, choose the safer and more robust design.

- All deployment targets MUST be under the direct ownership and control

of the NOVAX TRAVEL owner, not the Implementation Agent.

1. INPUT HANDLING – FULL EXTRACTION & DEEP SCAN

You receive ONE main ZIP archive uploaded by the owner.

This archive may contain:

- Documents (Word, PDF, text, markdown…)

- JSON/YAML configs

- OpenAPI specs

- SQL files

- RBAC / permissions definitions

- UI/UX drafts, images, logo files

- Yemen domain data, seeds, and configuration

- Other ZIP / 7z archives inside

Mandatory first steps:

1. FULL EXTRACTION

- Fully extract the main ZIP into a working directory.

- Recursively extract ALL nested ZIP/7z archives.

- Do NOT ignore any compressed file.

- Maintain a clear folder structure while extracting.

2. DEEP SCAN (HARD ANALYSIS)

- Perform a HARD DEEP SCAN over ALL files and folders.

- Read every file, every folder, every nested archive.

- Parse line-by-line, including:

- System specs

- Architecture descriptions

- OpenAPI & API definitions

- SQL schemas

- RBAC definitions

- UI/UX specs and notes

- Branding and logo files

- Yemen domain data, seeds, and configuration

- Build an internal, unified understanding of the complete NOVAX TRAVEL system.

3. DATA EXTRACTION

- From ALL files, extract and consolidate:

- Business rules

- Data models & entities

- API endpoints & contracts

- Roles, permissions, and RBAC rules

- Security, logging, monitoring requirements

- UI/UX expectations and flows

- Offline / sync rules for mobile

- All important constants, settings, and enums

- If you find conflicts between files, resolve them using best practices and

consistency across the whole system, giving priority to the most recent and

security-focused specs.

2. BRANDING & GLOBAL UI / UX

The owner will provide a logo and brand assets INSIDE the ZIP.

GLOBAL BRANDING

- Derive a full design system from the logo and brand:

- Primary / secondary colors

- Typography system

- Buttons, inputs, cards, layouts

- Create a WORLD-CLASS, VISUALLY STRIKING UI that is:

- Modern, clean, global

- Suitable for a Yemeni/global travel brand

- Consistent across Web, Mobile, and Admin

- Support dual theme (Light + Dark) if the specs require it.

The public homepage MUST include at minimum:

- Hero section with strong travel imagery (e.g. airplane, destinations).

- Prominent search module (from/to, dates, passengers, Search button).

- Sections for Special Offers and Popular / Upcoming Destinations.

- Clear top navigation (Flights, Hotels, Cars, Deals, Support, Sign In).

- Structured footer with About, Help, My Account, and Social links.

UI TARGETS

- Public Web App (Customer site)

- Mobile App (Android, primary platform; offline-friendly)

- Admin Panel (Operations, agents, finance, support)

- (If specified) Super Admin / System Creator panel

DELIVERABLES

- Production-ready UI code for:

- Web Frontend (Next.js / React or equivalent)

- Admin Panel (Web frontend)

- Mobile App (Flutter or equivalent cross-platform, Android-focused)

- Optional (recommended): a design-system export (Figma-like or design docs)

inside NOVAX_ASEM.zip for future designers.

3. OPENAPI – UNIFICATION & STANDARDIZATION

- Locate ALL OpenAPI / API definition files (YAML / JSON / Markdown / etc.).

- Parse and understand every endpoint, schema, and contract.

- Build ONE unified, clean, complete OpenAPI specification for:

- NOVAX TRAVEL public APIs (customer app)

- Internal admin/operations APIs

- Eliminate duplicates, resolve naming conflicts, and ensure consistency.

- Enforce:

- Clear resource naming

- Proper HTTP verbs and status codes

- Standardized error responses

- Pagination, filtering, sorting where appropriate

- Authentication and RBAC hooks on every protected endpoint.

OUTPUT PATHS (inside NOVAX_ASEM.zip)

- /api/openapi_novax_public.yaml

- /api/openapi_novax_admin.yaml

4. RBAC – FULL MERGE & CONSOLIDATION

- Discover ALL RBAC sources (JSON, YAML, SQL, docs).

- Merge them into ONE coherent RBAC model.

- Enforce least-privilege and clear separation of duties.

- Implement RBAC at:

- Database level (row-level constraints where appropriate).

- Backend API level (authorization on each endpoint).

- UI level in Admin/Superadmin panels.

Document RBAC as:

- /security/rbac_model.json

- /security/rbac_explained.md

5. DATABASE – FULL INTEGRATED SCHEMA

TARGET

- PostgreSQL (for deployment on Neon).

- Normalized, indexed, and optimized.

SCHEMA SCOPE (minimum)

- Users, authentication, sessions

- Roles & permissions (RBAC)

- Agents, companies, and B2B structures

- Flights, hotels, cars, visas, other travel services

- Bookings & itineraries

- Payments, invoices, refunds

- Wallet & loyalty points

- Notifications, logs, audit trails

- Admin & settings tables (system, branding, feature flags)

- Yemen-specific data (governorates, cities, local routes, local airlines)

- OTA mapping tables as required

DELIVERABLES

- /database/migrations/*.sql

- /database/schema_overview.md

6. FULL UI IMPLEMENTATION – WEB, MOBILE, ADMIN

WEB (CUSTOMER)

- Full booking funnels (search → select → book → pay) for flights, hotels, cars, visas.

- Account management (profile, booking history).

- Wallet & loyalty (earn + redeem).

- Support pages with WhatsApp/Telegram/email links.

- Multi-language support when specified (e.g., EN + AR).

ADMIN PANEL

- Dashboard with KPIs and charts.

- Booking management (search, filter, edit, cancel, refund).

- Payments & invoices.

- User, agent, company management.

- CMS-style content & configuration (banners, pages).

- Logs & audit views.

- Yemen-specific operations views (local routes, airlines) if specified.

MOBILE (ANDROID)

- Same customer flows as web.

- Offline-friendly (local cache for key data and Yemen dataset).

- Push notifications via Firebase or equivalent.

- Follows same branding and UX as web.

7. SECURITY, ENCRYPTION & PERFORMANCE

SECURITY

- Strong authentication & session management.

- Proper password hashing.

- Input validation & sanitization.

- OWASP Top 10 protections.

- Strict RBAC on every sensitive endpoint.

- Secrets only via environment variables.

- Logging without leaking secrets/tokens/passwords.

ENCRYPTION

- Encrypt sensitive data at rest (e.g. PII).

- Enforce HTTPS everywhere (behind Cloudflare or equivalent).

PERFORMANCE

- Efficient queries and proper indexing.

- Caching where appropriate.

- Pagination for large result sets.

- Optimized response times for real-world traffic.

Documentation:

- /security/security_architecture.md

- /performance/performance_notes.md

8. CLEANUP – DUPLICATION & CONFLICT RESOLUTION

- Remove or consolidate duplicated endpoints, schemas, RBAC entries, configs.

- Resolve conflicts by choosing the most robust, secure, scalable option.

- Ensure single sources of truth for:

- APIs (OpenAPI files)

- DB schema

- RBAC model

- Settings/constants

9. HOSTING, DOMAINS, EMAIL & ACCOUNTS

Use the owner’s existing accounts ONLY (no external provider-owned accounts):

- Domain & email (Hostinger)

- GitHub

- Neon (PostgreSQL)

- Cloudflare

- Render (backend hosting)

- Firebase

- Figma

Prepare for real deployment:

- Backend: Render

- Database: Neon

- Web frontend: Vercel or Render

- DNS/WAF/SSL: Cloudflare

- Auth/push: Firebase (if used)

- Email sending: Hostinger SMTP (or equivalent)

Use environment variables for:

- DB connection

- SMTP

- External API keys

Provide:

- /deploy/.env.example

- /deploy/deployment_guide.md

10. FINAL OUTPUT – NOVAX_ASEM.zip (STRUCTURE)

NOVAX_ASEM.zip MUST contain:

- Full backend source code

- Full frontend (web) source code

- Full admin panel source code

- Mobile app source (Android-focused)

- Unified OpenAPI specs

- Unified DB migrations

- Unified RBAC model

- Security & performance docs

- Deployment guide and .env examples

- Any design system / Figma-style exports or UI docs

- Seeds / demo data (including Yemen dataset if present)

11. SUPER ADMIN – MASTER OPERATIONS & PLAYBOOK FILE

Create:

- /superadmin/SUPERADMIN_OPERATIONS_GUIDE.md

This guide MUST include:

- System overview and environments.

- Access & security flows (Admin, Super Admin).

- RBAC overview, how to manage roles & permissions.

- Safe access management for staff, agents, companies, partners.

- Security best practices (passwords, MFA, key rotation).

- Feature flags & settings management.

- Data & DB operations without SQL (how migrations/releases affect DB).

- Deployments & releases (GitHub → Render/Vercel, rollback steps).

- Monitoring & incidents (dashboards, metrics, incident checklist).

- Backups & recovery.

- Compliance & audit (logs, export for legal reasons).

- Yemen-specific operations:

- Update routes, airlines, cities, fares.

- Manage local-only products (internal routes, offers).

- FAQ for Super Admin (common tasks).

12. LIVE DEPLOYMENT & DIRECT ACCESS REQUIREMENTS

This is NOT a prototype-only request.

The delivery must deliver a fully working, live, production-ready NOVAX TRAVEL system

that the owner can access via real URLs and an Android app, without writing code.

LIVE WEB ACCESS

- Deploy public site with the owner’s accounts (Render/Vercel + Cloudflare + Hostinger).

- Configure DNS for:

- https://www.novaxtravel.com

or a clearly documented equivalent (e.g., https://app.novaxtravel.com).

- Ensure all main flows are working in production.

ADMIN & SUPER ADMIN ACCESS

- Deploy Admin (and Super Admin) panel to a secure URL, for example:

- https://admin.novaxtravel.com

or:

- https://www.novaxtravel.com/admin

- Create an initial Super Admin account (temporary credentials).

- Document credentials in:

- /superadmin/SUPERADMIN_CREDENTIALS.md

- Include instructions for:

- First login

- Changing password

- Enabling MFA (if available)

ANDROID APPLICATION (APK)

- Build NOVAX TRAVEL Android app in RELEASE mode.

- Produce at least one signed APK:

- /mobile/releases/NOVAX_TRAVEL_PRODUCTION.apk

- (Recommended) Provide a download link on the public site or document how to host the APK.

SANDBOX vs PRODUCTION INTEGRATIONS

- Where real keys are not provided, use sandbox/test environments.

- Clearly label sandbox usage in:

- /deploy/deployment_guide.md

- Booking and payment flows MUST function logically using test data.

OWNER EXPERIENCE

- Owner can:

- Open the public site and complete bookings end-to-end.

- Log in to Admin/Super Admin and manage the platform.

- Install and use the Android APK for main flows.

- No coding, CLI, or SQL required for everyday operations.

13. PROVIDER AUTHENTICATION STRATEGY

- Prefer interactive LOGIN / OAuth flows (GitHub, Neon, Render, Cloudflare, Firebase, etc.).

- Only request API keys/tokens when interactive login is not possible.

- The owner will complete login forms manually when requested.

- All credentials and tokens MUST be stored only in the owner’s environments

and configuration, never in any the Implementation Agent–controlled infrastructure.

CHAPTER 204 – ADVANCED SECURITY, OBSERVABILITY, CI/CD & BUSINESS CONTINUITY

This chapter strengthens the NOVAX TRAVEL build mandate with additional

requirements around security hardening, observability, automated delivery,

testing, privacy, and business continuity. These requirements are MANDATORY and

apply to the entire NOVAX_ASEM.zip system and its live deployments.

1. OBSERVABILITY, LOGGING, METRICS & ALERTING

The delivery must implement a full observability layer that allows the OWNER to monitor

the health, performance, and reliability of NOVAX TRAVEL without writing code.

1. LOGGING

- Implement structured logging in all backend services.

- Log at minimum:

- Request/response metadata (without sensitive payloads).

- Authentication events (login, logout, failed attempts).

- Security events (access denied, suspicious patterns).

- System errors and exceptions.

- DO NOT log passwords, raw payment data, secrets, or full personal

documents in any form.

- Provide log views through:

- The hosting platform dashboards (Render, Neon, etc.), and/or

- A simple web-based log viewer in the Admin or Super Admin panel.

2. METRICS

- Collect and expose key metrics, including at minimum:

- Request rate, error rate, and latency per service.

- Database query duration and error rate.

- Background job throughput and failures (if jobs/queues are used).

- Present core metrics in an ADMIN/SUPERADMIN dashboard section as charts

and counters, so the OWNER can see system health at a glance.

3. ALERTING

- Design an alerting model where critical failures can trigger alerts

(for example via email) to the OWNER.

- At minimum, define conditions for:

- Service down / unreachable.

- Error rate above a defined threshold.

- Unusually high authentication failures (possible attack).

- Document how to configure alert destinations (email addresses) inside:

- /superadmin/SUPERADMIN_OPERATIONS_GUIDE.md

4. TRACES (OPTIONAL BUT RECOMMENDED)

- If supported by the chosen stack and OWNER accounts, implement basic

request tracing to follow a request across services.

- Any external observability services MUST be tied to accounts owned and

controlled by the OWNER, not the Implementation Agent.

2. CI/CD – AUTOMATED DELIVERY PIPELINES

The delivery must implement a CI/CD model based on the OWNER'S GitHub repository and

Render/Vercel deployment targets. the Implementation Agent must not use its own repositories

or any external code hosting; all code MUST live in OWNER-controlled GitHub.

1. VERSION CONTROL

- Initialize or update a Git repository under the OWNER'S GitHub account.

- Organize the repository (monorepo or multi-repo) according to best

practices, but always under OWNER control.

2. BRANCHING MODEL

- Define at minimum:

- main (production)

- develop (staging / pre-production)

- Document the branching and release model in:

- /docs/DEVELOPMENT_AND_RELEASE_MODEL.md

3. PIPELINES

- Configure GitHub Actions (or equivalent) to:

- Run automated tests on every push and pull request.

- Build backend, frontend, and mobile components as needed.

- Deploy to staging on merges to develop.

- Deploy to production on merges to main, with a manual approval gate

or clear instructions for triggering deployments.

- Pipelines MUST be configured to deploy only to environments in OWNER

Render/Vercel/Neon accounts.

4. DATABASE MIGRATIONS IN CI/CD

- Integrate database migrations into the deployment process so that schema

changes are applied safely:

- Apply migrations automatically in staging.

- Apply migrations in production with a safe, documented process

(including backup/restore and rollback steps).

All CI/CD configuration files (e.g., .github/workflows/*.yml) MUST be included

inside NOVAX_ASEM.zip and documented in the deployment guide.

3. TESTING STRATEGY & QUALITY GATES

The delivery must define and implement a basic, but real, testing strategy:

1. UNIT TESTS

- Implement unit tests for critical business logic (e.g. pricing, loyalty,

booking state transitions).

- Ensure unit tests run in CI on every commit.

2. INTEGRATION TESTS

- Implement integration tests for key flows:

- Authentication (login, logout, RBAC restrictions).

- Booking creation and modification.

- Payment workflow in sandbox/test mode.

3. END-TO-END (E2E) TESTS (MINIMUM SMOKE TESTS)

- Provide a small set of E2E smoke tests for:

- Search → Select → Book → Confirm (test data).

- Admin login → view dashboard → view booking details.

- These may be run manually or via CI as the OWNER prefers, but MUST be

documented.

4. QUALITY GATES

- CI MUST fail if:

- Tests fail.

- Linting / static analysis detects severe issues (where tooling is used).

Describe the testing strategy in:

- /docs/TESTING_STRATEGY.md

4. SECURITY HARDENING & WAF/RATE LIMITING

In addition to previous security requirements, you MUST:

1. CLOUDLFARE / WAF CONFIGURATION

- Define recommended Web Application Firewall (WAF) rules at Cloudflare

level, including at minimum:

- Blocking known malicious patterns.

- Basic DDoS mitigation (leveraging Cloudflare protections).

- Document recommended rules and settings for the OWNER inside:

- /security/CLOUDFLARE_WAF_RECOMMENDATIONS.md

2. RATE LIMITING

- Implement rate limiting at the API gateway or backend level for:

- Authentication endpoints (login, password reset).

- Sensitive APIs prone to abuse (e.g., search, pricing).

- Use safe default limits and make them configurable via environment

variables or admin settings where reasonable.

3. SECURITY HEADERS

- Ensure the web frontend and APIs return secure HTTP headers

(HSTS, X-Frame-Options, Content-Security-Policy where applicable)

following best practices.

4. SECRETS MANAGEMENT

- Confirm that all secrets are injected via environment variables

provided by OWNER-controlled platforms.

- No secrets may be hard-coded or stored in source control.

5. DATA PRIVACY, RETENTION & USER RIGHTS

The delivery must design NOVAX TRAVEL data flows with privacy and data minimization

principles in mind.

1. DATA MINIMIZATION

- Only store data that is actually needed for travel operations and legal

requirements.

- Avoid storing full payment card details or any highly sensitive data

beyond what is strictly necessary and compliant.

2. RETENTION POLICIES

- Define and document high-level retention rules for:

- Logs.

- Bookings and financial records.

- User profiles.

- Document these rules in:

- /docs/DATA_RETENTION_AND_PRIVACY_OVERVIEW.md

3. USER RIGHTS

- Implement admin capabilities to:

- Export a user’s data (for account owner requests).

- Anonymize or delete personal data where allowed by law and where it

does not conflict with legal/financial retention requirements.

- These capabilities MUST be accessible from the Admin/Super Admin UI.

6. BACKUP, DISASTER RECOVERY & RTO/RPO

Strengthen the business continuity model as follows:

1. BACKUPS

- Configure Neon backup capabilities (including built-in PITR if available).

- Define and document:

- Backup frequency.

- How to verify backups are working.

- Document backup strategy and steps in:

- /security/BACKUP_AND_RECOVERY_PLAN.md

2. DISASTER RECOVERY

- Define at a minimum:

- RTO (Recovery Time Objective) – target maximum downtime in a disaster.

- RPO (Recovery Point Objective) – target maximum data loss window.

- Document a step-by-step DR scenario in the Super Admin guide so the

OWNER knows what to do in a critical incident.

3. CONFIGURATION BACKUPS

- Ensure that critical configuration (environment variables templates,

DNS/WAF recommended settings, CI/CD configuration) are preserved in

documentation and version control (without exposing secrets).

7. AI ASSISTANT (OPTIONAL BUT RECOMMENDED)

If the attached ZIP and specifications request an AI-powered assistant for

NOVAX TRAVEL, then you MUST implement it in a way that does NOT compromise

security, privacy, or system integrity:

1. SCOPE

- The AI assistant may help users with:

- Finding flights/hotels/routes.

- Explaining booking policies.

- Guiding through support flows.

- It MUST NOT:

- Access or expose raw secrets, tokens, or internal configs.

- Execute arbitrary code.

- Bypass RBAC or data access restrictions.

2. INTEGRATION

- Any external AI API keys MUST be provided by the OWNER and stored only

in OWNER-controlled environments via environment variables.

- The assistant MUST respect RBAC and only surface information that the

current user is allowed to see.

3. DOCUMENTATION

- Document the AI assistant architecture, limitations, and configuration

in:

- /ai/AI_ASSISTANT_OVERVIEW.md

If no AI assistant is requested in the attached specs, this section may be

ignored; otherwise it is mandatory.

8. DOCUMENTATION SET COMPLETENESS

In addition to all previous chapters, you MUST ensure that NOVAX_ASEM.zip

contains at least the following documentation set, aligned with the final

implemented system:

- /deploy/deployment_guide.md

- /deploy/.env.example

- /database/schema_overview.md

- /security/security_architecture.md

- /security/BACKUP_AND_RECOVERY_PLAN.md

- /security/CLOUDFLARE_WAF_RECOMMENDATIONS.md

- /performance/performance_notes.md

- /security/rbac_explained.md

- /docs/TESTING_STRATEGY.md

- /docs/DEVELOPMENT_AND_RELEASE_MODEL.md

- /docs/DATA_RETENTION_AND_PRIVACY_OVERVIEW.md

- /superadmin/SUPERADMIN_OPERATIONS_GUIDE.md

- /superadmin/SUPERADMIN_CREDENTIALS.md (with temporary initial credentials)

All documentation MUST match the actual implemented system and MUST be written

in clear, simple technical English suitable for a non-programmer OWNER.

# ========================================

# CHAPTER 205 – ADVANCED SECURITY, UI/UX & TECHNICAL ENHANCEMENTS

# ========================================

## 205.1 ENHANCED SECURITY FRAMEWORK

### 205.1.1 Two-Factor Authentication (2FA)

- All admin and user accounts must support 2FA via:

- TOTP (Google Authenticator, Authy)

- SMS-based OTP (for Yemeni numbers where technically feasible)

- Backup codes for recovery

- 2FA is mandatory for:

- Super Admin accounts

- Financial transactions

- Sensitive data exports

- Any access to Super Admin / security configuration areas

### 205.1.2 Advanced API Security

- Implement CSRF tokens for all state-changing requests (web sessions).

- Use API rate limiting per user/IP (recommended default: 100 requests/minute, configurable).

- Validate all incoming requests with signed JWT tokens (for API clients).

- Enable CORS only for trusted domains and subdomains owned by the OWNER.

- Enforce strict input validation and schema validation on all external APIs.

### 205.1.3 Data Encryption

- Encrypt all sensitive data at rest using AES-256 or equivalent industry standard.

- Use TLS 1.3 for all data in transit (via Cloudflare / hosting platform).

- Encrypt database backups before storage.

- Ensure encryption keys are managed ONLY via OWNER-controlled environment configuration.

### 205.1.4 Threat Monitoring & IDS

- Integrate with an intrusion detection solution (e.g. OSSEC/Wazuh or equivalent) where supported.

- Log all security events to a dedicated Security Event stream / SIEM-like sink.

- Set up automatic alerts for at least:

- Multiple failed login attempts.

- Unusual API traffic patterns.

- Unauthorized access attempts.

- All monitoring and alerting accounts must be created under OWNER control.

### 205.1.5 Backup & Disaster Recovery

- Daily automated backups of at least:

- Database (full + incremental if supported).

- User-uploaded documents.

- System configuration files (without secrets).

- Store backups in geographically separate locations or storage classes where possible.

- Test restore procedures at least quarterly and document test results.

- NEVER use production backups directly in non-production environments without anonymization.

## 205.2 UI/UX ENHANCEMENTS

### 205.2.1 Responsive Design

- Mobile-first approach for all interfaces.

- Breakpoints (minimum recommendation):

- Mobile: < 768px

- Tablet: 768px – 1024px

- Desktop: > 1024px

- Use CSS Grid/Flexbox (or equivalent layout system in chosen framework) for layouts.

### 205.2.2 Accessibility (WCAG 2.1 AA Compliance)

- Screen reader support (ARIA labels and semantic HTML structure).

- Keyboard navigation support for all interactive elements.

- Sufficient color contrast (minimum 4.5:1 for text).

- Text resizing up to 200% without breaking layout.

### 205.2.3 Performance Optimization

- Implement lazy loading for images and heavy components.

- Minify CSS, JS, and HTML in production builds.

- Use CDN for static assets (via Cloudflare or equivalent).

- Enable Gzip/Brotli compression on all HTTP responses where supported.

- Target (under normal load):

- Page load time < 3 seconds on standard broadband/4G.

- API p95 latency < 500 ms for typical queries.

### 205.2.4 User Experience Features

- Dark/Light mode toggle (persisted per user or device).

- Language switcher (Arabic/English) with full RTL/LTR support:

- All layouts, components, and typography must correctly adapt to RTL in Arabic.

- Session timeout warning (e.g. 10-minute warning before logout for inactivity).

- Offline indicator with auto-sync status for mobile and web where offline caching is used.

### 205.2.5 Legal & Policy Pages

- Generate initial, editable templates and public pages for:

- Privacy Policy

- Terms & Conditions / Terms of Use

- Cookies / Data Usage Notice (if applicable)

- Expose these pages at standard URLs (e.g. /privacy, /terms, /cookies) and link them:

- In the footer of the public site.

- In relevant onboarding / account creation flows.

- Content must be easily editable by the OWNER via CMS or configuration files.

## 205.3 PERFORMANCE & SCALABILITY

### 205.3.1 Database Optimization

- Implement read replicas for high-traffic read queries where supported.

- Use database indexing on frequently queried columns based on actual query patterns.

- Partition large tables (e.g., audit_logs, request_logs) by date or tenant where appropriate.

### 205.3.2 Caching Strategy

- Use Redis or an equivalent cache for:

- Session storage (where not handled by managed auth).

- Frequently accessed data (airlines, routes, pricing, static Yemen data).

- Implement cache invalidation hooks on data updates to avoid stale results.

- Use edge caching via Cloudflare for public, cacheable endpoints and static content.

### 205.3.3 Horizontal Scalability

- Design all stateless services so they can be scaled horizontally.

- Use message queues (e.g., RabbitMQ/Redis or hosting equivalent) for asynchronous tasks:

- Email sending, notifications, heavy background processing.

- Implement auto-scaling (where platform supports it) based on CPU/memory/latency thresholds.

## 205.4 COMPLIANCE & DOCUMENTATION

### 205.4.1 GDPR/Data Protection and Local Laws

- Implement user data anonymization for analytics where possible.

- Implement a "Right to be forgotten" process, respecting legal/financial retention requirements.

- Provide data processing agreement templates or documentation for B2B partners where relevant.

- Never use real production PII/payment data in development or staging; use anonymized or synthetic data.

- Clearly document data flows and storage locations in:

- /docs/DATA_RETENTION_AND_PRIVACY_OVERVIEW.md

### 205.4.2 API Documentation

- Provide Swagger/OpenAPI documentation for all endpoints.

- Include clear example requests/responses.

- Include authentication examples (JWT headers, cookies, etc.).

- Ensure the API docs are accessible via:

- A protected admin route, and/or

- Static files inside NOVAX_ASEM.zip for offline reference.

### 205.4.3 User & Admin Manuals

- Provide interactive guides for critical workflows using a guided tour library (e.g., Shepherd.js or equivalent) where feasible.

- Provide short video tutorials or step-by-step guides for complex workflows (booking management, refunds, agent setup), even if only as links/placeholders.

- Provide an FAQ section with search for:

- End users (public site).

- Admin/agents (inside Admin/Super Admin panel).

## 205.5 MONITORING & ANALYTICS

### 205.5.1 System Monitoring

- Implement uptime monitoring (e.g., UptimeRobot or equivalent) for:

- Public site.

- Admin panel.

- API endpoints.

- Implement error tracking (e.g., Sentry or equivalent) integrated with the OWNER'S accounts.

- Implement performance monitoring (e.g., New Relic/Datadog or equivalent) where supported by OWNER accounts.

### 205.5.2 Business Analytics & BI

- Integrate with Google Analytics 4 (or equivalent) for web analytics, under OWNER's property.

- Provide custom dashboards for at least:

- Conversion rates (search → booking).

- User engagement (active users, repeat visits).

- Revenue tracking (daily/weekly/monthly).

- Top routes/destinations and top-performing agents/companies.

- Unpaid/overdue invoices and refunds.

- Where feasible, expose these KPIs in an Admin/BI dashboard inside the Admin/Super Admin panel.

## 205.6 MOBILE APP ENHANCEMENTS

### 205.6.1 Offline-First Architecture

- Use an offline-first approach for the mobile app where critical flows allow it.

- Use local storage/SQLite or equivalent for:

- Cached bookings.

- Static datasets (Yemen cities, routes, airlines, etc.).

- Implement background sync for pending requests as connectivity is restored.

- Implement local database versioning and migration for the mobile app.

### 205.6.2 Push Notifications

- Use Firebase Cloud Messaging (FCM) for Android push notifications.

- Use local notifications for offline alerts where appropriate (reminders, sync status).

- Provide per-user notification preferences (topics: bookings, offers, system alerts).

## 205.7 DEPLOYMENT & CI/CD

### 205.7.1 Environment Separation

- Maintain at least three isolated environments:

- Development

- Staging

- Production

- Each environment must have isolated databases and configuration.

- Document how to promote releases from Development → Staging → Production.

### 205.7.2 Automated Testing

- Implement automated Unit tests (e.g., Jest/PHPUnit or equivalent stack tools).

- Implement Integration tests for key flows (auth, booking, payments in sandbox).

- Implement E2E tests (e.g., Cypress or equivalent) for main user journeys.

- Ensure all these tests are integrated into CI pipelines as quality gates.

## 205.8 FINAL CHECKLIST FOR IMPLEMENTATION AGENT

- [ ] Implement all security measures from 205.1.

- [ ] Apply UI/UX enhancements from 205.2, including legal/policy pages and RTL.

- [ ] Configure performance and scalability optimizations from 205.3 with target SLOs.

- [ ] Generate all compliance and documentation assets from 205.4.

- [ ] Set up monitoring and analytics from 205.5 under OWNER accounts only.

- [ ] Enhance the mobile app per 205.6 with offline-first and FCM.

- [ ] Finalize CI/CD pipeline per 205.7 on OWNER GitHub + Render/Vercel/Neon.

- [ ] Verify that all external tools (monitoring, analytics, error tracking) are connected only to OWNER-controlled accounts.

# ========================================

# END OF CHAPTER 205

# ========================================

# ========================================

# CHAPTER 206 – SUPER ADMIN NO-CODE CONTROL PANEL

# ========================================

## 206.1 PRINCIPLES

The NOVAX TRAVEL owner (SUPER ADMIN) MUST be able to operate and evolve the

platform **without writing SQL or code**.

All day-to-day changes to data, settings, reference tables, and business rules

MUST be performed through **safe, validated web interfaces**, not through

direct database access.

Direct SQL access to the production database is **strictly forbidden** for

normal operations. All structural change and data updates MUST go through:

- Controlled migration mechanisms, or

- Safe, validated Super Admin UI flows.

## 206.2 MANAGED DATA VIA SUPER ADMIN UI

The SUPER ADMIN CONTROL PANEL MUST provide dedicated screens/modules that allow

the OWNER to create, edit, deactivate, or delete records for at least the

following data categories, **without writing SQL**:

1. Reference & Domain Data

- Yemen governorates, cities, airports, routes.

- Local airlines and carriers.

- International destinations (where defined).

- Static lookup tables (countries, currencies, languages, etc.).

2. Product & Pricing Configuration

- Flight, hotel, car, visa products and categories.

- Base prices, markups, fees, commissions, and discounts.

- Promotional campaigns, coupons, and special offers.

- Service fees and extra charges.

3. Accounts & Access

- Agents and companies, including:

- Creation, suspension, and termination.

- Commission rules and credit limits.

- Roles and permissions assignment (within the RBAC model defined earlier).

- Staff accounts (Admin, Finance, Support, etc.).

4. Content & Branding

- Banners, sliders, home page sections.

- Static pages (About, Help, FAQ, Policies).

- Contact details (phone, WhatsApp, Telegram, email, social links).

- Logo, theme colors, and visual branding settings.

5. System & Operational Settings

- Feature flags (enable/disable modules).

- Booking rules (cancellation windows, penalties, deadlines).

- Payment settings (available methods, test vs live modes).

- Notification templates (email, SMS, push, WhatsApp).

All of the above MUST be configurable via UI forms with validation and

permissions checks, and MUST be reflected in the database automatically.

## 206.3 SAFE CHANGE MODEL (NO RAW SQL)

To prevent damage to the system, the following rules apply:

1. NO RAW SQL IN PRODUCTION

- The Super Admin MUST NOT need to run SQL statements manually.

- The system MUST NOT expose any “execute SQL” feature in the UI.

2. VALIDATED FORMS & WORKFLOWS

- Every Super Admin change must go through validated forms that:

- Enforce required fields.

- Validate data types and ranges.

- Prevent inconsistent or unsafe values.

- Where a change may have large impact (e.g., deleting a city, airline,

or product), the system MUST:

- Show clear warnings.

- Require explicit confirmation (e.g., type-to-confirm).

3. VERSIONED CONFIGURATION

- System configuration changes (pricing rules, feature flags, critical

booking logic) SHOULD be versioned where feasible, so that:

- Old configurations can be inspected.

- Rollback is possible for misconfigurations.

4. AUDIT LOGS

- All Super Admin actions that change data or settings MUST be logged with:

- Who made the change.

- When it was made.

- What was changed (before/after snapshot or equivalent summary).

## 206.4 SUPER ADMIN CONFIGURATION CONSOLE – MODULES

The SUPER ADMIN panel MUST include, at minimum, the following modules as

first-class navigation sections:

1. **Data Management**

- UI for managing all reference tables (Yemen data, lookups, routes).

- Bulk import/export capabilities (CSV/Excel) with validation, where safe.

2. **Business Rules & Pricing**

- UI for managing markups, commissions, fees, and discount rules.

- Simulation tools (optional but recommended) to test pricing scenarios

without affecting live bookings.

3. **Access & Security**

- UI for managing staff, agents, companies.

- UI for assigning/removing roles and permissions (within the RBAC model).

- UI for enforcing 2FA/MFA policies and password policies.

4. **Content & UI Configuration**

- UI to manage texts, promotions, banners, home sections, and legal pages.

- UI to switch languages and edit translations (where supported).

- UI to manage branding (colors, logos, favicon, etc.).

5. **System Settings**

- UI for environment-level toggles (test/sandbox vs production for payments).

- UI for notification channels and templates.

- UI for setting operational thresholds (e.g., timeout values, limits,

SLA-related parameters).

## 206.5 GUARANTEES FOR SUPER ADMIN EXPERIENCE

the Implementation Agent MUST guarantee that, upon delivery:

- The OWNER (Super Admin) can:

- Operate NOVAX TRAVEL fully from the UI.

- Add, update, and deactivate data and configurations without SQL.

- Adjust prices, offers, and booking rules safely.

- Update Yemen-specific data as needed.

- No day-to-day operational task will require:

- Writing SQL queries.

- Editing code.

- Direct database access.

Any task that still requires code or SQL MUST be explicitly documented in the

Super Admin guide as an **exception**, with a clear explanation and recommended

workflow for requesting technical support when needed.

# ========================================

# END OF CHAPTER 206 – SUPER ADMIN NO-CODE CONTROL PANEL

# ========================================

# ========================================

# ========================================

# ========================================

# CHAPTER 207 – CUSTOMER FEEDBACK & RATING SYSTEM

# ========================================

## 207.1 SYSTEM NOMENCLATURE & CORE CONCEPT

### 207.1.1 Naming Convention

- PRIMARY NAME: "تقييم الخدمة" (Service Rating)

- ADMIN PANEL: "تقييمات العملاء" (Customer Ratings)

- USER INTERFACE: "شاركنا رأيك" (Share Your Feedback)

- DATABASE PREFIX: "rating_"

### 207.1.2 Core Principles

- VOLUNTARY: Users choose to rate

- VERIFIED: Only actual customers can rate

- TRANSPARENT: Show all approved ratings

- RESPONSIVE: Admin responds within 24h

## 207.2 DATABASE ARCHITECTURE

### 207.2.1 Main Rating Table

```sql

-- Main ratings table

CREATE TABLE customer_ratings (

id BIGSERIAL PRIMARY KEY,

uuid VARCHAR(36) UNIQUE NOT NULL DEFAULT gen_random_uuid(),

-- Relations

booking_id BIGINT NOT NULL REFERENCES bookings(id) ON DELETE CASCADE,

user_id BIGINT NOT NULL REFERENCES users(id) ON DELETE CASCADE,

service_id BIGINT NOT NULL, -- Dynamic reference (flight_id, hotel_id, etc)

service_type VARCHAR(20) NOT NULL CHECK (service_type IN ('flight', 'hotel', 'car', 'visa', 'general')),

-- Ratings (1-5 stars)

overall_rating SMALLINT NOT NULL CHECK (overall_rating BETWEEN 1 AND 5),

service_quality SMALLINT CHECK (service_quality BETWEEN 1 AND 5),

value_for_money SMALLINT CHECK (value_for_money BETWEEN 1 AND 5),

agent_support SMALLINT CHECK (agent_support BETWEEN 1 AND 5),

ease_of_booking SMALLINT CHECK (ease_of_booking BETWEEN 1 AND 5),

-- Feedback text

title VARCHAR(150),

review_text TEXT,

admin_reply TEXT,

-- Media

photos JSONB DEFAULT '[]', -- Array of image URLs

allow_photos BOOLEAN DEFAULT false,

-- Metadata

is_verified BOOLEAN DEFAULT true, -- User actually booked

is_featured BOOLEAN DEFAULT false,

is_anonymous BOOLEAN DEFAULT false,

status VARCHAR(20) DEFAULT 'pending' CHECK (status IN ('pending', 'approved', 'rejected', 'hidden')),

-- Engagement

helpful_count INTEGER DEFAULT 0,

report_count INTEGER DEFAULT 0,

view_count INTEGER DEFAULT 0,

-- Timestamps

created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,

updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,

replied_at TIMESTAMP WITH TIME ZONE,

-- Indexes for performance

INDEX idx_rating_service (service_type, service_id),

INDEX idx_rating_status (status),

INDEX idx_rating_user (user_id),

INDEX idx_rating_created (created_at DESC)

);

```

### 207.2.2 Rating Categories Table

```sql

-- Service-specific rating categories

CREATE TABLE rating_categories (

id SERIAL PRIMARY KEY,

category_key VARCHAR(50) UNIQUE NOT NULL,

service_type VARCHAR(20) NOT NULL,

name_ar VARCHAR(100) NOT NULL,

name_en VARCHAR(100) NOT NULL,

description_ar TEXT,

description_en TEXT,

is_active BOOLEAN DEFAULT true,

is_required BOOLEAN DEFAULT false,

sort_order INTEGER DEFAULT 0,

created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP

);

-- Default categories

INSERT INTO rating_categories (category_key, service_type, name_ar, name_en, is_required) VALUES

('aircraft_cleanliness', 'flight', 'نظافة الطائرة', 'Aircraft Cleanliness', true),

('crew_service', 'flight', 'خدمة المضيفين', 'Crew Service', true),

('comfort', 'flight', 'الراحة', false),

('punctuality', 'flight', 'الالتزام بالمواعيد', true),

('room_cleanliness', 'hotel', 'نظافة الغرفة', 'Room Cleanliness', true),

('hotel_location', 'hotel', 'موقع الفندق', 'Hotel Location', true),

('staff_service', 'hotel', 'خدمة الموظفين', 'Staff Service', true),

('driver_service', 'car', 'خدمة السائق', 'Driver Service', true),

('car_condition', 'car', 'حالة السيارة', 'Car Condition', true),

('processing_speed', 'visa', 'سرعة المعالجة', 'Processing Speed', true);

```

### 207.2.3 Category Ratings Table

```sql

-- Detailed category ratings

CREATE TABLE rating_category_scores (

id BIGSERIAL PRIMARY KEY,

rating_id BIGINT NOT NULL REFERENCES customer_ratings(id) ON DELETE CASCADE,

category_id INTEGER NOT NULL REFERENCES rating_categories(id) ON DELETE CASCADE,

score SMALLINT NOT NULL CHECK (score BETWEEN 1 AND 5),

created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

UNIQUE(rating_id, category_id)

);

```

### 207.2.4 Rating Helpful/Report Table

```sql

-- Track helpful votes and reports

CREATE TABLE rating_engagements (

id BIGSERIAL PRIMARY KEY,

rating_id BIGINT NOT NULL REFERENCES customer_ratings(id) ON DELETE CASCADE,

user_id BIGINT NOT NULL REFERENCES users(id) ON DELETE CASCADE,

action_type VARCHAR(20) NOT NULL CHECK (action_type IN ('helpful', 'report', 'share')),

reason VARCHAR(100), -- For reports

created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

UNIQUE(rating_id, user_id, action_type)

);

```

## 207.3 USER INTERFACE COMPONENTS

### 207.3.1 Rating Trigger System

```javascript

// Rating trigger logic

const ratingTriggers = {

triggers: [

{

name: 'post_booking',

condition: 'booking_status == "completed"',

delay: '24_hours',

max_attempts: 3,

channels: ['email', 'sms', 'app_notification']

},

{

name: 'booking_history',

condition: 'user_views_booking_history',

always_show: true,

position: 'after_booking_details'

},

{

name: 'mobile_app',

condition: 'app_opened_after_completion',

delay: 'immediate',

channels: ['in_app']

}

],

// Trigger rating request

triggerRating: function(bookingId, userId, serviceType) {

// Check if already rated

// Check timing conditions

// Send appropriate notification

}

};

```

### 207.3.2 Rating Form Components

```jsx

// React Component for Rating Form

const RatingForm = ({ bookingId, serviceType, serviceId }) => {

// Core rating elements

const formElements = [

{

type: 'overall_stars',

label: 'التقييم العام',

required: true,

component: FiveStarRating

},

{

type: 'category_ratings',

label: 'التقييم التفصيلي',

component: CategoryRatings,

dependsOn: serviceType

},

{

type: 'quick_feedback',

label: 'ملاحظات سريعة',

component: SentimentButtons,

options: ['ممتاز', 'جيد', 'متوسط', 'ضعيف']

},

{

type: 'text_review',

label: 'اكتب رأيك',

component: TextArea,

maxLength: 500,

placeholder: 'شاركنا تجربتك...'

},

{

type: 'photo_upload',

label: 'إضافة صور',

component: PhotoUpload,

maxFiles: 3,

maxSize: '5MB'

},

{

type: 'privacy_settings',

label: 'إعدادات الخصوصية',

component: PrivacyToggle,

options: [

{ value: 'public', label: 'عرض باسمي' },

{ value: 'anonymous', label: 'عرض كعميل نوفاكس' },

{ value: 'private', label: 'خاص (لإدارة نوفاكس فقط)' }

]

}

];

return <FormBuilder elements={formElements} />;

};

```

## 207.4 ADMIN DASHBOARD MODULES

### 207.4.1 Rating Management Dashboard

```text

Admin Route: /admin/ratings

Layout: Master-Detail with sidebar filters

MAIN COMPONENTS:

1. Overview Cards (Top):

- Total Ratings: 1,234

- Average Rating: 4.2/5

- Pending Review: 23

- Response Rate: 85%

2. Filter Panel (Left Sidebar):

- Status: All | Pending | Approved | Rejected

- Service Type: All | Flights | Hotels | Cars | Visa

- Rating Score: 5★ | 4★ | 3★ | 2★ | 1★

- Date Range: Last 7 days | Last 30 days | Custom

- Verification: All | Verified | Unverified

- Featured: All | Featured Only

3. Ratings List (Main Area):

- Compact card for each rating

- Shows: User Avatar, Rating Stars, Brief Review, Date

- Quick actions: Approve/Reject/Feature/Reply

4. Bulk Actions:

- Select multiple ratings

- Actions: Approve Selected, Reject Selected, Delete, Export

```

### 207.4.2 Analytics Dashboard

```javascript

// Analytics Dashboard Metrics

const ratingAnalytics = {

metrics: {

overall: {

title: 'التقييم العام',

value: '4.2',

trend: '+0.3',

data: [4.1, 4.0, 4.2, 4.3, 4.2, 4.1, 4.2]

},

volume: {

title: 'عدد التقييمات',

value: '1,234',

trend: '+15%',

data: [120, 135, 110, 145, 130, 125, 140]

},

response: {

title: 'معدل الرد',

value: '85%',

trend: '+5%',

data: [80, 82, 85, 83, 87, 85, 85]

},

satisfaction: {

title: 'معدل الرضا',

value: '92%',

trend: '+2%',

data: [90, 91, 92, 93, 92, 91, 92]

}

},

charts: [

{

type: 'bar',

title: 'توزيع التقييمات',

data: {

'5★': 554,

'4★': 370,

'3★': 185,

'2★': 86,

'1★': 39

}

},

{

type: 'line',

title: 'التقييمات حسب الشهر',

data: [

{ month: 'يناير', flights: 4.3, hotels: 4.1, cars: 4.0 },

{ month: 'فبراير', flights: 4.4, hotels: 4.2, cars: 4.1 },

{ month: 'مارس', flights: 4.5, hotels: 4.3, cars: 4.2 }

]

},

{

type: 'pie',

title: 'التقييمات حسب الخدمة',

data: {

flights: 650,

hotels: 320,

cars: 180,

visa: 84

}

}

]

};

```

### 207.4.3 Real-time Monitoring

```yaml

Real-time Alerts Configuration:

critical_alerts:

- condition: rating <= 2

channels: [email, sms, push]

recipients: [admin, manager, support]

response_time: 1_hour

- condition: rating contains ['سيء', 'أسوأ', 'غش', 'سرقة']

channels: [email, dashboard]

recipients: [admin, legal]

response_time: 2_hours

warning_alerts:

- condition: rating == 3

channels: [email]

recipients: [support]

response_time: 24_hours

- condition: no_response_48h

channels: [email]

recipients: [support]

response_time: immediate

dashboard_widgets:

- new_ratings_today: "عرض التقييمات الجديدة لحظياً"

- low_ratings_pending: "التقييمات المنخفضة قيد المعالجة"

- average_response_time: "متوسط زمن الرد"

- top_rated_services: "الخدمات الأعلى تقييماً"

```

## 207.5 PUBLIC DISPLAY SYSTEM

### 207.5.1 Service Page Rating Display

```html

<!-- Flight/Hotel Detail Page Component -->

<div class="service-rating-widget">

<div class="rating-summary">

<div class="average">

<div class="stars">★★★★☆</div>

<div class="score">4.2 <span>من 5</span></div>

<div class="count">(1,234 تقييم)</div>

</div>

<div class="distribution">

<div class="bar-row">

<span>5 نجوم</span>

<div class="bar"><div class="fill" style="width: 45%"></div></div>

<span>45%</span>

</div>

<!-- Repeat for 4, 3, 2, 1 stars -->

</div>

</div>

<div class="category-ratings">

<h4>التقييم التفصيلي:</h4>

<div class="category">

<span>نظافة الطائرة</span>

<div class="rating">4.3/5</div>

</div>

<!-- More categories -->

</div>

<button class="write-review">اكتب تقييمك</button>

</div>

```

### 207.5.2 Reviews Listing Page

```javascript

// Reviews List Component Configuration

const reviewsListConfig = {

pagination: {

itemsPerPage: 10,

loadMore: true,

infiniteScroll: true

},

sorting: [

{ value: 'newest', label: 'الأحدث' },

{ value: 'highest', label: 'الأعلى تقييماً' },

{ value: 'lowest', label: 'الأدنى تقييماً' },

{ value: 'most_helpful', label: 'الأكثر فائدة' }

],

filters: [

{ type: 'rating', label: 'التقييم', options: ['5 نجوم', '4 نجوم', '3 نجوم'] },

{ type: 'service', label: 'الخدمة', options: ['طيران', 'فنادق', 'سيارات'] },

{ type: 'date', label: 'التاريخ', options: ['أخر أسبوع', 'أخر شهر', 'أخر 3 أشهر'] }

],

reviewCard: {

show: ['user_avatar', 'user_name', 'rating_stars', 'review_text', 'date', 'service_info'],

actions: ['helpful', 'report', 'share'],

truncateText: 200,

showMoreText: 'عرض المزيد'

}

};

```

## 207.6 AUTOMATION RULES & WORKFLOWS

### 207.6.1 Auto-Moderation Rules

```yaml

automation_rules:

auto_approve:

conditions:

- rating >= 4

- review_length > 20

- no_blacklisted_keywords

- user_has_previous_approved_ratings

action: "approve_immediately"

flag_for_review:

conditions:

- rating <= 2

- contains_any: ['سيء', 'غش', 'سرقة', 'مشكلة', 'شكوى']

- multiple_exclamation_marks: '!!!'

- same_ip_multiple_ratings

action: "flag_to_admin"

auto_response:

trigger: "rating_approved"

conditions:

- rating >= 4: "شكراً لك على تقييمك الإيجابي!"

- rating == 3: "نشكرك على ملاحظاتك. سنعمل على تحسين خدماتنا."

- rating <= 2: "نعتذر عن تجربتك. فريق الدعم سيتواصل معك."

```

### 207.6.2 Email & Notification Templates

```yaml

email_templates:

rating_request:

subject: "كيف كانت تجربتك مع نوفاكس؟"

body: |

مرحباً {user_name},

نأمل أن تكون رحلتك/إقامتك كانت ممتعة.

نود معرفة رأيك في الخدمة لتساعدنا على التحسين.

{rating_link}

شكراً لثقتك بنوفاكس.

thank_you_rating:

subject: "شكراً لك على مشاركة رأيك!"

body: |

عزيزي {user_name},

نشكرك على أخذ الوقت لتقييم خدماتنا.

ملاحظاتك قيمة وتساعدنا على تقديم خدمة أفضل.

admin_alert_low_rating:

subject: "تنبيه: تقييم منخفض ({rating} نجوم)"

body: |

تنبيه إداري:

المستخدم: {user_name}

الخدمة: {service_type} - {service_name}

التقييم: {rating} نجوم

الرابط: {admin_link}

```

## 207.7 REPORTING SYSTEM

### 207.7.1 Standard Reports

```sql

-- Monthly Rating Report

SELECT

DATE_TRUNC('month', r.created_at) AS report_month,

s.service_type,

COUNT(*) AS total_ratings,

ROUND(AVG(r.overall_rating), 2) AS avg_rating,

COUNT(CASE WHEN r.overall_rating >= 4 THEN 1 END) AS positive_ratings,

COUNT(CASE WHEN r.overall_rating <= 2 THEN 1 END) AS negative_ratings,

ROUND(COUNT(CASE WHEN r.admin_reply IS NOT NULL THEN 1 END) * 100.0 / COUNT(*), 2) AS response_rate,

ROUND(AVG(CASE WHEN r.overall_rating <= 2 THEN EXTRACT(EPOCH FROM (r.replied_at - r.created_at))/3600 END), 2) AS avg_response_hours

FROM customer_ratings r

LEFT JOIN (

SELECT DISTINCT service_type, service_id

FROM customer_ratings

) s ON r.service_id = s.service_id

WHERE r.status = 'approved'

AND r.created_at >= DATE_TRUNC('month', CURRENT_DATE - INTERVAL '6 months')

GROUP BY report_month, s.service_type

ORDER BY report_month DESC, s.service_type;

```

### 207.7.2 Export Functionality

```javascript

// Export configuration

const exportConfig = {

formats: [

{

name: 'Excel',

type: 'xlsx',

columns: [

'ID', 'User', 'Service', 'Rating', 'Review', 'Date', 'Status'

]

},

{

name: 'CSV',

type: 'csv',

columns: [

'id', 'user_email', 'service_type', 'rating', 'review', 'created_at'

]

},

{

name: 'PDF Report',

type: 'pdf',

template: 'rating_summary',

includes: ['charts', 'summary', 'details']

}

],

scheduling: {

daily: 'summary_daily',

weekly: 'full_report_weekly',

monthly: 'detailed_report_monthly'

}

};

```

## 207.8 INTEGRATION POINTS

### 207.8.1 With Booking System

```yaml

integration:

booking_completion:

trigger: "booking.status = 'completed'"

action: "queue_rating_request"

delay: "24_hours"

booking_details:

display: "show_rating_button"

condition: "booking_is_older_than_24h"

position: "booking_history_page"

agent_performance:

link: "ratings.agent_id = agents.id"

metrics: ["avg_rating", "response_time", "customer_satisfaction"]

```

### 207.8.2 With Notification System

```javascript

// Notification integration

const ratingNotifications = {

channels: {

email: {

template: 'rating_alert',

recipients: ['admin@novaxtravel.com', 'support@novaxtravel.com']

},

sms: {

template: 'urgent_rating_alert',

recipients: ['+967XXXXXXXXX'],

condition: 'rating <= 2'

},

push: {

template: 'new_rating',

recipients: 'admin_app_users',

condition: 'always'

}

},

timing: {

immediate: ['rating <= 2', 'contains_complaint'],

hourly_digest: ['all_ratings'],

daily_summary: ['statistics']

}

};

```

## 207.9 MOBILE APP INTEGRATION

### 207.9.1 Flutter Rating Components

```dart

// Flutter Rating Widgets

class NovaRatingWidgets {

// Star rating widget

static Widget starRating({

required double rating,

required Function(double) onRatingChanged,

int starCount = 5,

double size = 30.0,

Color color = Colors.amber,

}) {

return StarRating(

rating: rating,

onRatingChanged: onRatingChanged,

starCount: starCount,

size: size,

filledStar: Icon(Icons.star, color: color),

halfStar: Icon(Icons.star_half, color: color),

emptyStar: Icon(Icons.star_border, color: color),

);

}

// Review card widget

static Widget reviewCard({

required Review review,

bool showFull = false,

Function()? onHelpful,

Function()? onReport,

}) {

return Card(

child: Padding(

padding: EdgeInsets.all(12.0),

child: Column(

crossAxisAlignment: CrossAxisAlignment.start,

children: [

// User info and stars

Row(

children: [

CircleAvatar(

backgroundImage: review.isAnonymous

? null

: NetworkImage(review.userAvatar),

child: review.isAnonymous

? Text(review.userInitials)

: null,

),

SizedBox(width: 10),

Expanded(

child: Column(

crossAxisAlignment: CrossAxisAlignment.start,

children: [

Text(

review.isAnonymous

? 'عميل نوفاكس'

: review.userName,

style: TextStyle(fontWeight: FontWeight.bold),

),

starRating(rating: review.rating, onRatingChanged: (double _) {}),

],

),

),

Text(

DateFormat('dd/MM/yyyy').format(review.date),

style: TextStyle(color: Colors.grey, fontSize: 12),

),

],

),

SizedBox(height: 10),

// Review text

Text(

showFull ? review.text : review.getPreviewText(),

maxLines: showFull ? null : 3,

overflow: showFull ? null : TextOverflow.ellipsis,

),

// Actions

Row(

children: [

IconButton(

icon: Icon(Icons.thumb_up_outlined),

onPressed: onHelpful,

tooltip: 'مفيد',

),

Text('${review.helpfulCount}'),

Spacer(),

if (!showFull)

TextButton(

onPressed: () => _showFullReview(review),

child: Text('عرض المزيد'),

),

],

),

],

),

),

);

}

}

```

### 207.9.2 Offline Support

```dart

// Offline rating storage

class OfflineRatingManager {

final LocalDatabase _localDb;

Future<void> saveRatingOffline(RatingData rating) async {

await _localDb.insert('pending_ratings', {

'id': rating.id ?? DateTime.now().millisecondsSinceEpoch,

'booking_id': rating.bookingId,

'rating': rating.overallRating,

'review': rating.reviewText,

'photos': jsonEncode(rating.photos),

'created_at': DateTime.now().toIso8601String(),

'status': 'pending_sync',

});

}

Future<void> syncPendingRatings() async {

final pending = await _localDb.getAll('pending_ratings');

for (var rating in pending) {

try {

await _api.submitRating(rating);

await _localDb.delete('pending_ratings', rating['id']);

} catch (e) {

// Keep for next sync attempt

}

}

}

}

```

## 207.10 IMPLEMENTATION CHECKLIST (WITHOUT TIME SCHEDULE)

```yaml

phase_1_core_system:

database:

- [ ] Create customer_ratings table

- [ ] Create rating_categories table

- [ ] Create rating_category_scores table

- [ ] Create rating_engagements table

backend:

- [ ] Rating submission API

- [ ] Rating retrieval API

- [ ] Basic admin endpoints

frontend:

- [ ] Rating form component

- [ ] Star rating widget

- [ ] Basic review display

phase_2_admin_dashboard:

admin_panel:

- [ ] Ratings list with filters

- [ ] Rating approval/rejection

- [ ] Admin reply system

- [ ] Bulk operations

analytics:

- [ ] Basic statistics dashboard

- [ ] Rating distribution charts

- [ ] Export functionality

moderation:

- [ ] Auto-moderation rules

- [ ] Flagging system

- [ ] Spam detection

phase_3_public_features:

public_display:

- [ ] Service page rating widget

- [ ] Reviews listing page

- [ ] Sorting and filtering

- [ ] Search functionality

user_features:

- [ ] Helpful voting

- [ ] Review reporting

- [ ] Photo upload

- [ ] Privacy controls

integration:

- [ ] Email notifications

- [ ] Booking system integration

- [ ] Mobile app integration

phase_4_advanced_features:

advanced_analytics:

- [ ] Sentiment analysis

- [ ] Trend detection

- [ ] Predictive analytics

- [ ] Custom reports

automation:

- [ ] Smart reply suggestions

- [ ] Auto-categorization

- [ ] Performance alerts

- [ ] Scheduled reports

optimization:

- [ ] Performance optimization

- [ ] Caching strategy

- [ ] SEO optimization

- [ ] Accessibility improvements

```

## 207.11 SUCCESS METRICS & KPIs

### Quantitative Metrics

```yaml

performance_metrics:

participation:

target: "> 20% of completed bookings"

measurement: "ratings_count / completed_bookings"

rating_score:

target: "> 4.0/5.0 average"

measurement: "AVG(overall_rating)"

response_rate:

target: "> 80% of negative ratings"

measurement: "replied_ratings / total_negative_ratings"

response_time:

target: "< 24 hours for negative ratings"

measurement: "AVG(replied_at - created_at) for negative ratings"

```

### Qualitative Metrics

```yaml

quality_metrics:

review_quality:

measurement: "Average review length > 50 characters"

target: "> 60% of reviews"

user_engagement:

measurement: "Helpful clicks per review"

target: "> 0.5 helpful/review"

system_accuracy:

measurement: "False positive moderation rate"

target: "< 5%"

customer_satisfaction:

measurement: "Post-rating satisfaction survey"

target: "> 4.5/5.0"

```

### Business Impact Metrics

```yaml

business_metrics:

conversion_impact:

measurement: "Booking conversion with/without ratings"

target: "+15% with ratings"

retention_impact:

measurement: "Repeat customer rate"

target: "+20% for engaged reviewers"

service_improvement:

measurement: "Service rating improvement over time"

target: "+0.5/5.0 per year"

agent_performance:

measurement: "Agent rating correlation with performance"

target: "Strong positive correlation"

```

END OF CHAPTER 207

# CHAPTER 208 – CRITICAL MISSING FUNDAMENTALS

# ========================================

## 208.1 ABSOLUTELY REQUIRED SECURITY FIXES

### 208.1.1 Password Security (Missing in Docs)

- ENFORCE: Minimum 8 characters with uppercase, lowercase, number.

- BLOCK: Common passwords (like "123456", "password", "qwerty").

- REQUIRE: Password change every 90 days for admin users.

- PREVENT: Password reuse (last 5 passwords).

### 208.1.2 Session Security (Not Detailed Enough)

- SESSION TIMEOUT: 30 minutes inactivity → auto logout.

- SINGLE SESSION: One active session per user (configurable).

- SESSION FIXATION: Regenerate session ID after login.

- BROWSER VALIDATION: Session tied to browser/device fingerprint where feasible.

### 208.1.3 Input Validation (Critical Missing)

- SQL INJECTION: Parameterized queries ONLY, no raw SQL string concatenation.

- XSS PROTECTION: HTML encode and sanitize all user-controlled input before display.

- FILE UPLOAD:

- Restrict to [.jpg, .jpeg, .png, .pdf], max 5MB.

- Scan for viruses/malware where supported.

- EMAIL/PHONE/CONTACT:

- Validate email format and domain where possible.

- Validate phone number format according to country rules.

- Reject disposable/temporary email domains where feasible.

## 208.2 BASIC ERROR HANDLING (NOT SPECIFIED)

### 208.2.1 User-Friendly Errors

- DO NOT SHOW to users:

- Database errors.

- File paths.

- Code snippets or stack traces.

- DO SHOW to users:

- Generic message: "Something went wrong. Reference ID: XYZ123".

- LOG:

- Full error details with stack trace in server logs only.

- Include the same reference ID that is shown to the user.

### 208.2.2 HTTP Error Pages

- 404: Custom "Page not found" with search/suggestions and link back home.

- 403: "Access denied" with option to contact support/admin.

- 500: "Maintenance mode" or "Try again later" message.

- ALL: Include navigation back to home and minimal branding.

## 208.3 BASIC PERFORMANCE (MISSING BASICS)

### 208.3.1 Image Optimization (Not Mentioned)

- AUTO-RESIZE: Uploaded images resized to max 1920px width (configurable).

- WEBP FORMAT: Convert images to WebP for modern browsers where supported.

- LAZY LOAD: Images load only when visible in viewport.

- CDN: All images and static assets served via Cloudflare CDN or equivalent.

### 208.3.2 Database Indexing (Not Specified)

- REQUIRED INDEXES (minimum examples):

- users: email, phone_number.

- bookings: user_id, status, created_at.

- payments: booking_id, status.

- flights: origin, destination, departure_date.

- the Implementation Agent MUST review actual query patterns and add additional indexes as needed.

### 208.3.3 Basic Caching Strategy

- CACHE FOR 5 minutes:

- Flight search results (non-personalized).

- CACHE FOR 1 hour:

- Airline lists, city lists, static lookups.

- CACHE FOR 24 hours:

- Static content (FAQs, terms, policies) where appropriate.

- NEVER CACHE:

- User sessions.

- Payment pages.

- Highly sensitive or user-specific data.

## 208.4 MOBILE APP ESSENTIALS (MISSING)

### 208.4.1 Offline Mode Details

- STORE LOCALLY (where safe):

- User profile (non-sensitive fields).

- Recent searches.

- Booking drafts.

- SYNC: Automatically when back online.

- QUEUE: Actions performed offline queued and sent when online.

- INDICATOR: Clear offline/online status indicator in the app.

### 208.4.2 App Permissions (Not Specified)

- ASK FOR:

- Camera (e.g., upload receipts/documents).

- Storage (save tickets/itineraries).

- EXPLAIN clearly why each permission is needed.

- GRACEFUL DEGRADATION: App should still work with reduced features if permissions are denied.

## 208.5 BASIC ADMIN PANEL FEATURES (MISSING)

### 208.5.1 Bulk Operations (Not Mentioned)

- BULK ACTIONS:

- Update booking status.

- Send emails/SMS to filtered user groups.

- Export filtered data (CSV/Excel).

- TEMPLATES:

- Email/SMS templates for common messages (confirmation, reminder, cancellation).

- FILTERS:

- Ability to save and reuse filter combinations (e.g., "Today’s unpaid bookings").

### 208.5.2 Activity Feed (Not Specified)

- SHOW:

- Recent bookings, new users, payments, refunds.

- FILTER:

- By user, by date, by action type.

- SEARCH:

- Search across admin actions for audit and support purposes.

## 208.6 BASIC USER FEATURES (MISSING)

### 208.6.1 Search History (Not Mentioned)

- SAVE:

- Last 10 searches per user (or configurable).

- SHOW:

- "Recent searches" on search page (opt-in for privacy).

- CLEAR:

- Option for user to clear their search history.

### 208.6.2 Booking Management Basics

- CANCEL:

- Self-cancellation within defined time window (e.g., 24 hours) according to business rules.

- MODIFY:

- Ability to change passenger details or preferences before ticketing/issuance where permitted.

- DUPLICATE:

- Create a new booking from a previous one (re-booking flow).

- SHARE:

- Booking details via link/QR code where appropriate, with secure token-based access.

## 208.7 BASIC SYSTEM MONITORING (NOT SPECIFIED)

### 208.7.1 Health Checks (Missing)

- DAILY (automated or scheduled checks):

- Database connection.

- Disk space.

- Email sending / SMTP connectivity.

- External APIs (if used) basic reachability.

- ALERT:

- If any critical service fails 3 times in 10 minutes.

- DASHBOARD:

- Simple green/red status indicators for all core services.

### 208.7.2 Basic Analytics (Not Mentioned)

- TRACK (minimum):

- Daily bookings.

- Daily revenue.

- New registered users.

- COMPARE:

- Today vs yesterday.

- This week vs last week.

- SHOW:

- Simple line chart for last 30 days (at least) in Admin dashboard.

## 208.8 BASIC BACKUP (INSUFFICIENT DETAIL)

### 208.8.1 What to Backup Daily

- DATABASE:

- Full dump at a fixed time (e.g., 02:00 server time).

- UPLOADED FILES:

- Receipts, tickets, documents, user uploads.

- CONFIG (non-secret):

- Application configuration, feature flags, settings (without secrets).

### 208.8.2 Backup Verification

- WEEKLY:

- Test restore from backup in a non-production environment.

- MONITOR:

- Backup file size (alert if unexpectedly small or missing).

- ROTATION POLICY:

- Keep at least:

- 7 daily backups.

- 4 weekly backups.

- 12 monthly backups.

## 208.9 BASIC LEGAL REQUIREMENTS (MISSING)

### 208.9.1 Required Pages (Not Specified)

- TERMS OF SERVICE:

- Booking terms, cancellation policy, refund rules.

- PRIVACY POLICY:

- What data is collected, how it is used, retention basics.

- CONTACT PAGE:

- Email, phone, address (or at least owner’s official contact methods).

- COOKIE / TRACKING POLICY:

- Explain cookies and tracking technologies used.

### 208.9.2 User Consent (Not Mentioned)

- REQUIRE:

- Users must accept terms before first booking.

- RECORD:

- Date/time and version of terms accepted.

- UPDATE:

- Require re-acceptance when terms change significantly.

## 208.10 BASIC ACCESSIBILITY (NOT SPECIFIED)

### 208.10.1 Minimum Requirements

- ALT TEXT:

- All meaningful images must have descriptive alt text.

- CONTRAST:

- Text color contrast ratio ≥ 4.5:1 for normal text.

- KEYBOARD:

- All core functions must be accessible via keyboard only.

- FOCUS:

- Visible focus indicator for all interactive elements.

## 208.11 IMPLEMENTATION PRIORITY LIST

### MUST DO BEFORE LAUNCH

1. [ ] Password security rules (208.1.1).

2. [ ] SQL injection and XSS protection (208.1.3).

3. [ ] Basic error pages (404, 403, 500) (208.2.2).

4. [ ] Image optimization/resizing (208.3.1).

5. [ ] Required database indexes (208.3.2).

6. [ ] Basic caching strategy (208.3.3).

7. [ ] Privacy Policy & Terms pages (208.9.1).

8. [ ] Contact page with real contact info (208.9.1).

### FIRST WEEK AFTER LAUNCH

1. [ ] Session timeout and session security (208.1.2).

2. [ ] Activity feed for admin (208.5.2).

3. [ ] Basic health monitoring (208.7.1).

4. [ ] Daily backup system with rotation (208.8.1–208.8.2).

5. [ ] Search history for users (208.6.1).

### FIRST MONTH AFTER LAUNCH

1. [ ] Mobile app offline mode refinements (208.4.1).

2. [ ] Bulk operations in admin (208.5.1).

3. [ ] Basic analytics dashboard enhancements (208.7.2).

4. [ ] Accessibility improvements (208.10.1).

5. [ ] Extended booking management features (208.6.2).

# ========================================

# END OF CHAPTER 208 – CRITICAL MISSING FUNDAMENTALS

CHAPTER 209 – FINAL COMPLETION & MISSING SPEC PACKAGE

This chapter closes ALL remaining gaps in the NOVAX TRAVEL

Master Execution Document and delivers the final missing

technical artifacts required for a 100% autonomous build by

the Implementation Agent.

It is MANDATORY and OVERRIDES NOTHING. It only COMPLETES

the system.

209.1 FULL DATABASE MIGRATION PACKAGE (MANDATORY)

the Implementation Agent MUST generate FULL SQL migrations for ALL systems.

Required standards:

- PostgreSQL-compatible

- Soft deletes where appropriate

- Indexes on foreign keys

- JSONB for flexible fields

- UTC timestamps

- Referential integrity enforced

Mandatory table groups:

1. USERS & IDENTITY

users, roles, permissions, user_role_map,

mfa_configs, devices, login_attempts

2. AGENCIES & COMPANIES

agencies, sub_agencies, companies,

company_employees, monthly_budget tracking

3. REQUEST ENGINE

requests, request_states, request_documents,

request_messages, sla_trackers, audit_logs

4. FLIGHTS

airlines, yemen_cities, yemen_governorates,

yemen_routes, flight_schedules, flight_fares,

passenger_profiles

5. HOTELS

hotels, hotel_rooms, hotel_prices, hotel_requests

6. CARS

car_drivers, car_routes, car_requests

7. VISAS

visa_countries, visa_requirements, visa_requests

8. FINANCIAL

wallet_transactions, loyalty_points,

commission_rules, pricing_rules, invoices,

receipts, cost_logs

9. SYSTEM

system_settings, feature_flags,

notification_templates, security_events,

data_access_logs, automation_flows,

automation_triggers

the provider MUST generate all migrations automatically based on

this chapter + previous structure.

209.2 OPENAPI / SWAGGER SPECIFICATION (MANDATORY)

the Implementation Agent MUST auto-generate an OpenAPI 3.1 spec covering:

- ALL endpoints

- ALL request/response schemas

- ALL authentication flows

- ALL pagination rules

- ALL object definitions

Minimum endpoints:

AUTH:

POST /auth/register

POST /auth/login

POST /auth/logout

POST /auth/refresh

POST /auth/mfa/verify

FLIGHTS:

GET /flights/search

POST /flights/book

POST /flights/ticket/upload

REQUESTS:

GET /requests

GET /requests/{id}

POST /requests/{id}/state

POST /requests/{id}/payment-verify

PRICING:

GET /pricing/rules

POST /pricing/rules

WALLET:

GET /wallet

POST /wallet/credit

POST /wallet/debit

NOTIFICATIONS:

GET /notifications

POST /notifications/test

ADMIN:

ALL CRUD endpoints for:

- agencies

- companies

- airline management

- dataset management

- pricing engine

- automation engine

- system settings

209.3 OFFLINE SYNC CONFLICT RULESET (FINAL SPEC)

the provider MUST implement strict conflict resolution rules:

1. USER DATA

Server wins for profile fields.

Client keeps drafts.

2. REQUESTS

If request exists on both sides:

- Compare updated_at timestamp

- Newer version wins

- Combine missing fields when non-conflicting

3. PRICING RULES & DATASETS

Server always wins.

4. FAILED SYNC OPERATIONS

Client enters "pending_sync" state and retries

with exponential backoff.

5. DOCUMENTS

If duplicate upload:

Latest checksum wins.

209.4 FRAUD DETECTION MATRIX (MANDATORY SPEC)

the provider MUST integrate Fraud Score Calculation.

Scoring (0–100):

- IP Risk                      (0–20)

- Device Fingerprint Mismatch (0–15)

- Repeated Payment Failures   (0–15)

- Multiple Accounts per Device(0–10)

- Suspicious Route Patterns   (0–10)

- Too Many Requests/Minute    (0–15)

- Passport Document Issues    (0–15)

Fraud Score Actions:

0–30   Allow

31–60  Require MFA

61–80  Manual Review

81–100 Auto-block + alert admin

209.5 UNIVERSAL CONFIG FILE (central-config.json)

the provider MUST generate a GLOBAL config file:

{

"version": "1.0.0",

"base_currency": "USD",

"loyalty_ratio": "1 USD = 1 point",

"loyalty_redeem": "500 points = 1 USD",

"default_airport": "ADE",

"enable_guest_mode": true,

"enable_notifications": true,

"otp_method": "email",

"fraud_detection_level": "medium",

"offline_sync_interval": 30,

"pricing_engine": {

"priority_rules": true,

"bundle_rules": true

},

"ai_assistant": {

"enabled": true,

"mode": "safe_operations",

"restricted_fields": [

"password",

"api_keys",

"credentials"

]

}

}

209.6 AI MODULE SPECIFICATION (FINAL)

The AI assistant must:

- Help users find flights, hotels, cars, visas

- Guide through booking steps

- Route complex issues to human admin

- NEVER see or access:

- passwords

- API keys

- system credentials

- Operate in SAFE MODE only

- Be embedded inside Web + App + Admin

209.7 CI/CD ACTUAL PIPELINES (FINAL)

the provider MUST auto-generate:

backend.yml:

- install PHP deps

- run tests

- run migrations check

- deploy to Render

web.yml:

- npm install

- next build

- deploy to Vercel

admin.yml:

- same as web.yml + RBAC test

mobile.yml:

- flutter build apk

- upload to Backblaze

- update OTA metadata

209.8 FINAL EXECUTION GUARANTEE

the Implementation Agent MUST:

- Execute autonomously

- Build 100% of the system

- Deploy all services

- Seed all datasets

- Generate documentation

- Produce the final ZIP package

- Deliver APK + credentials

- Ask ZERO technical questions

END OF CHAPTER 209

CHAPTER 210 – DEPLOYMENT AUTHENTICATION & OWNER ACCESS POLICY

This chapter defines the mandatory authentication and access-control protocol between the Owner and the Implementation Agent for REAL production deployment.

210.1 Core Principle

the Implementation Agent MUST NOT deploy, configure, or connect to any external infrastructure provider without explicitly requesting authentication from the Owner at the exact moment it is required.

210.2 Mandatory Providers Requiring Explicit Authentication

the Implementation Agent must pause execution and request authentication for each of the following providers individually:

- Render (Backend Hosting)

- Vercel (Web & Admin Hosting)

- Neon (PostgreSQL Database)

- Backblaze B2 (Object Storage)

- Cloudflare (DNS, SSL, WAF)

- Firebase (Push Notifications)

210.3 Authentication Request Protocol

For each provider, the Implementation Agent must issue a clear request in the following format:

“Please provide login link, API token, or temporary authentication code for [PROVIDER NAME].”

the Implementation Agent MUST:

- Wait for Owner response

- Validate authentication success

- Proceed only after confirmation

- Never reuse credentials across providers

210.4 Security & Control Rules

- the Implementation Agent must not store plaintext credentials.

- All secrets must be injected via secure environment variables.

- Access must be scoped to deployment and configuration tasks only.

- Owner retains full ownership and revocation rights at all times.

210.5 Deployment Blocking Rule

If authentication is not provided for a required provider, the Implementation Agent MUST:

- Stop deployment for that provider

- Continue with non-dependent tasks only

- Clearly report pending authentication status in execution logs

210.6 Execution Guarantee

By including this chapter, the Owner guarantees controlled, secure, step-by-step deployment, while the Implementation Agent guarantees zero deployment without explicit authorization.

This chapter is mandatory and overrides any implicit deployment behavior.

210.7 Completion Acceptance شرط قبول الإنجاز

Completion is NOT accepted unless novaxtravel.com and www.novaxtravel.com resolve to the production Web, SSL is valid, and you provide the exact DNS records used plus a final verification report.

210.8 Production Delivery Package شرط تسليم الإنتاج

Completion is NOT accepted unless the Implementation Agent delivers a final package containing:

1) Production URLs:

- Web: https://novaxtravel.com and https://www.novaxtravel.com

- Admin: a dedicated admin URL (or /admin) with confirmed access

- API: https://api.novaxtravel.com (or the final backend production URL)

2) Admin Credentials:

- Super Admin email + temporary password

- Mandatory password change enforced on first login

3) OpenAPI Documentation URL or exported file.

4) Database connection verification (Neon) and migration status report.

210.9 DNS & SSL Verification شرط DNS و SSL

the Implementation Agent must provide the exact DNS records used (A/AAAA/CNAME) for:

- @ (root domain)

- www

- api (if used)

Completion is NOT accepted unless:

- DNS resolves globally,

- SSL is valid (no warnings),

- and the provider provides a final verification report (timestamped).

210.10 Backup & Rollback Safety شرط الأمان والرجوع

Before switching novaxtravel.com to production, the Implementation Agent must:

1) Enable automated DB backups (Neon) and confirm retention settings.

2) Provide a rollback plan:

- How to revert DNS to previous state

- How to rollback backend/web deploy to last stable release

3) Confirm secrets are stored only in provider env variables (never in code).

Completion is NOT accepted without this safety plan.

210.11 Observability & Health Checks شرط المراقبة

the Implementation Agent must implement production health endpoints and monitoring:

- /health (API) must return DB, cache, queue, storage status.

- Admin Panel must include a "System Health" page.

- Alerts must be configured for: downtime, error rate spikes, DB connection failures.

Completion is NOT accepted unless monitoring + alerts are enabled and tested.

210.12 Email Deliverability (SMTP + DNS) شرط البريد

the Implementation Agent must configure transactional email and deliverability:

- Configure SMTP provider (Hostinger/other) for OTP and notifications.

- Provide required DNS records for SPF, DKIM, and DMARC.

Completion is NOT accepted unless a real test email is delivered successfully.

210.12.1 OTP Email Sender Identity & Inbound Policy (Mandatory)

Goal:

OTP emails MUST be sent from:

- From Address: info@novaxtravel.com

- From Name: NOVAX TRAVEL

And the info@ mailbox MUST NOT accept inbound emails.

A) SMTP / APP CONFIG (Non-Negotiable)

the Implementation Agent MUST configure the transactional email sender as:

- MAIL_FROM_ADDRESS = "info@novaxtravel.com"

- MAIL_FROM_NAME    = "NOVAX TRAVEL"

- MAIL_REPLY_TO      = "support@novaxtravel.com"   (customers who reply must go to support, not OTP channel)

Rules:

- The system MUST force the From identity; no user-controlled "from" values.

- OTP emails MUST be queued (background job) with rate-limits to prevent abuse.

- Email content MUST NOT include any secrets besides the OTP code itself.

- Provide real delivery test proof in production (timestamp + recipient).

B) INBOUND DISABLEMENT FOR info@ (Mandatory)

the Implementation Agent MUST ensure info@ does not receive incoming emails using one of these acceptable methods:

Option 1 (Preferred): Reject inbound at mail server level

- Configure mailbox/alias policy to return:

550 "This mailbox does not accept inbound email. Please contact support@novaxtravel.com"

- Ensure no storage is consumed.

Option 2: Auto-delete inbound (if reject is not supported)

- Create a server-side rule/filter on info@:

- If inbound message received -> immediately delete (or move to trash) with no forwarding.

Additional mandatory settings:

- Disable catch-all for the domain.

- Do not forward inbound from info@ to any personal mailbox.

C) DNS DELIVERABILITY (Mandatory)

the Implementation Agent MUST provide and apply the exact DNS records required for:

- SPF (authorize the chosen SMTP provider)

- DKIM (provider DKIM keys enabled)

- DMARC (minimum: p=quarantine; recommended: p=reject after validation)

Completion is NOT accepted unless:

- A real OTP email is delivered successfully to a real mailbox

- From shows: "NOVAX TRAVEL <info@novaxtravel.com>"

- Reply goes to: support@novaxtravel.com

- info@ inbound is confirmed rejected or auto-deleted

NOVAX TRAVEL – OTP EMAIL TEMPLATE (PRODUCTION)

SENDER IDENTITY (MANDATORY)

- From Name: NOVAX TRAVEL

- From Email: info@novaxtravel.com

- Reply-To: support@novaxtravel.com

- Inbound Policy for info@novaxtravel.com: REJECT inbound (preferred) or AUTO-DELETE

A) ENGLISH TEMPLATE

SUBJECT:

NOVAX TRAVEL – Your Verification Code

PREHEADER (optional):

Use this code to complete your sign-in. It expires soon.

BODY (HTML or TEXT):

Hello {{customer_name_or_hello}},

Your NOVAX TRAVEL verification code is:

{{otp_code}}

This code will expire in {{otp_expiry_minutes}} minutes.

If you did not request this code, please ignore this email.

Need help? Contact us at support@novaxtravel.com

Thank you,

NOVAX TRAVEL

FOOTER (optional compliance):

You are receiving this email because you are verifying access to your NOVAX TRAVEL account.

B) ARABIC TEMPLATE (RTL-READY)

SUBJECT:

NOVAX TRAVEL – رمز التحقق الخاص بك

PREHEADER (اختياري):

استخدم هذا الرمز لإكمال تسجيل الدخول. سينتهي قريبًا.

BODY (HTML or TEXT):

مرحباً {{customer_name_or_hello}}،

رمز التحقق الخاص بك في NOVAX TRAVEL هو:

{{otp_code}}

سينتهي هذا الرمز خلال {{otp_expiry_minutes}} دقيقة.

إذا لم تطلب هذا الرمز، يمكنك تجاهل هذه الرسالة.

للمساعدة: support@novaxtravel.com

شكراً لك،

NOVAX TRAVEL

FOOTER (اختياري):

تصلك هذه الرسالة لأنك تقوم بعملية تحقق للدخول إلى حسابك في NOVAX TRAVEL.

C) SECURITY & UX RULES (MANDATORY)

1) OTP code MUST be digits-only or short alphanumeric (Owner choice), default 6 digits.

2) OTP expiry MUST be configurable, default 10 minutes.

3) Rate limiting MUST apply:

- max attempts per OTP

- max OTP requests per user/IP per time window

4) Do NOT include any links that reveal secrets.

5) Do NOT include passwords or account details.

6) Emails MUST not be sent from any address other than info@novaxtravel.com.

END OF OTP EMAIL TEMPLATE

210.13 Production Protection شرط الحماية

the Implementation Agent must enforce:

- API rate limits per IP/user/agent

- WAF rules (Cloudflare) for common attacks

- Brute-force login protection + lockouts

Completion is NOT accepted unless protection rules are enabled and verified.

210.14 Staging Before Domain Cutover شرط الاختبار قبل الدومين

the Implementation Agent must deploy a staging environment and validate core flows

(login, search, request creation, admin access) before switching novaxtravel.com.

Completion is NOT accepted unless staging verification is documented.

210.15 Cost Control & Paid Actions Approval شرط التحكم بالتكلفة

the Implementation Agent must STOP and request owner approval before:

- upgrading any plan,

- enabling paid add-ons,

- increasing resource tiers,

- purchasing domains/certificates/services.

Completion is NOT accepted without a final cost estimate and confirmation.

END OF CHAPTER 210

CHAPTER 211 – POST-DEPLOYMENT GOVERNANCE, SECRET ROTATION & OWNER RUNBOOK

This chapter defines mandatory post-deployment governance, security hardening,

and owner-operational handover requirements. It is ADDITIVE and MUST be executed

after production deployment is completed.

211.1 Ownership Handover & Access Review (Mandatory)

the Implementation Agent MUST deliver a complete access inventory and ensure the Owner has full

control over all infrastructure accounts and resources.

the Implementation Agent MUST provide an "Access Inventory Report" listing, for EACH provider:

- Render: services, env vars, deploy settings, team members, tokens used

- Vercel: projects, domains, env vars, team members, tokens used

- Neon: database name(s), roles/users, connection strings (masked), backups status

- Backblaze B2: bucket(s), app keys used, lifecycle rules, public/private policies

- Cloudflare: zones, DNS records, SSL mode, WAF rules, API tokens used

- Firebase: project id, FCM config, service accounts/keys used (masked), app registrations

Handover Rules:

- The Owner MUST be added as the primary admin/owner where applicable.

- Any temporary users, shared tokens, or temporary access created during execution MUST be identified.

- the Implementation Agent MUST request Owner approval before disabling/removing any access, then proceed to:

- Remove temporary users

- Revoke temporary tokens

- Confirm the system remains operational after revocation

Completion is NOT accepted unless the Access Inventory Report is delivered and

temporary access (if any) is revoked with Owner approval.

211.2 Secret Rotation & Security Hardening (Mandatory)

After deployment, the Implementation Agent MUST execute a formal secret rotation plan to ensure

no build-time or temporary secrets remain valid.

Secrets that MUST be rotated (as applicable):

- Backend application secrets (e.g., APP_KEY, JWT secret, encryption keys)

- Database credentials (Neon roles/passwords or tokens)

- SMTP credentials (Hostinger/other provider)

- Backblaze B2 application keys

- Cloudflare API tokens

- Firebase service account keys / tokens

- Any third-party integration keys (if configured)

Rotation Requirements:

- Generate new secrets using strong randomness.

- Update secrets ONLY via provider environment variables / secret managers.

- Never commit secrets into code or repositories.

- Validate system functionality after each rotation step:

- Login / MFA

- Requests flow

- Admin access

- File upload/download (storage)

- Email OTP / notifications

- Push notifications (if enabled)

Completion is NOT accepted unless secret rotation is completed and verified.

211.3 Owner Runbook & Minimal Operations Guide (Mandatory)

the Implementation Agent MUST deliver a short, Owner-friendly operational runbook that enables

non-technical operation without vendor support.

The Runbook MUST include:

1) Production URLs:

- Web (novaxtravel.com, www)

- Admin (final admin URL)

- API (final API URL)

2) Admin Access:

- How to log in as Super Admin

- How to reset passwords / enforce MFA

3) Daily Operations:

- Where to manage pricing rules

- Where to manage agencies/companies/budgets

- Where to review requests and states

- Where to manage content/datasets (Yemen data)

4) Monitoring & Incidents:

- Where to view "System Health" and alerts

- What to do if downtime occurs

- How to check /health and interpret status

5) Backups & Restore:

- Backup policy confirmation (Neon)

- Restore steps (high-level) and who can execute

6) Cost Control:

- Where to see usage/cost estimates

- What settings impact cost most (storage, bandwidth, DB size)

7) Change Management:

- How to deploy a safe update (staging → production)

- Rollback steps for Web/Admin/Backend and DNS

Completion is NOT accepted unless the Runbook is delivered as a final document

and the Owner confirms they can access Admin and view System Health.

211.4 Final Acceptance Criteria for Chapter 211

This chapter is considered complete ONLY when:

- Access Inventory Report is delivered

- Temporary access is revoked (with Owner approval)

- Secret rotation is completed and verified

- Owner Runbook is delivered and validated

END OF CHAPTER 211

CHAPTER 212 – LEGAL PAGES, CONSENT MANAGEMENT & POLICY VERSIONING

This chapter closes the remaining gap for production legality and compliance by

adding mandatory Legal Pages (Privacy/Terms) and a full Consent Logging system.

It is ADDITIVE and MUST be implemented across Web, Mobile, and Admin.

212.1 Scope and Mandatory Legal Artifacts

the Implementation Agent MUST implement the following end-user legal artifacts as real pages/screens:

1) Privacy Policy

2) Terms of Use / Terms of Service

3) Cookie/Tracking Notice (if cookies/analytics are used)

4) Contact & Legal Notices page (support email, company info, jurisdiction statement)

These artifacts MUST exist in:

- Web Portal (public pages)

- Mobile App (in-app screens)

- Admin Panel (management module)

212.2 Policy Versioning Model (Non-Negotiable)

All legal documents MUST be versioned and publishable.

Rules:

- Each policy has: doc_type, version, language, title, content, status (draft/published/archived),

effective_from, created_by, published_by, published_at, checksum/hash.

- Admin can publish a new version at any time.

- Older versions MUST remain accessible for audit (read-only) for at least 7 years.

212.3 Consent Capture Requirements (Mandatory)

The system MUST capture explicit user consent for:

- Terms of Use

- Privacy Policy

- (Optional) Marketing communications consent (separate toggle; default OFF)

- (Optional) Cookie/analytics consent (where applicable)

Consent MUST be collected:

- At registration / first login (blocking until accepted)

- Whenever a newer published version becomes effective (re-consent required)

- On any guest-to-registered upgrade flow

Consent UI rules:

- Separate checkboxes for Terms and Privacy (not bundled into one checkbox).

- Links to open the policy text before accepting.

- The system MUST prevent proceeding if mandatory consents are not accepted.

212.4 Consent Logging Data Structures (Mandatory)

the Implementation Agent MUST implement a consent logging subsystem with at least these tables:

A) legal_documents

- id (PK)

- doc_type (privacy/terms/cookies/notice)

- version (e.g., "1.0.0")

- language (e.g., "en", "ar")

- title

- content (HTML/Markdown)

- status (draft/published/archived)

- effective_from (UTC)

- checksum

- created_by, published_by

- created_at, published_at

B) user_consents

- id (PK)

- user_id (FK, nullable for guest if supported)

- doc_type

- doc_version

- accepted (boolean)

- accepted_at (UTC)

- source (web/mobile/admin)

- ip_address

- device_id (nullable)

- user_agent (nullable)

- locale (nullable)

- evidence_hash (hash of {doc_checksum + user_id + accepted_at + device_id})

C) consent_events (audit trail)

- id (PK)

- user_id

- event_type (accepted/declined/forced_reaccept/viewed)

- doc_type

- doc_version

- event_at (UTC)

- metadata (JSONB)

Retention:

- Consent logs MUST be retained for at least 7 years (not purged by normal log cleanup).

212.5 Admin Panel – Legal & Consent Management Module (Mandatory)

Admin Panel MUST include a dedicated module "Legal & Policies" that allows:

- Create/edit drafts of legal documents per language

- Preview formatting

- Publish a new version with effective_from

- Archive an old version

- View diffs between versions

- Rollback by re-publishing a prior version (new publish event still recorded)

Admin Panel MUST also include "User Consents" reporting:

- Search by user, date, doc_type, version

- Export CSV/JSON for audits

- View per-user timeline of consent events

- Show who published which versions and when

Permissions:

- legal.manage_documents

- legal.publish_documents

- legal.view_consents

- legal.export_consents

212.6 API Contracts (Mandatory)

the Implementation Agent MUST expose secure endpoints:

Public (no auth):

- GET /legal/documents?doc_type=terms&language=en  (returns latest published effective document)

- GET /legal/documents/versions?doc_type=terms     (returns published versions list)

Authenticated:

- POST /legal/consents/accept

body: { doc_type, doc_version, accepted:true, source, device_id, locale }

- GET /me/consents (returns user's current consent status and required re-consent flags)

Admin:

- CRUD endpoints for legal_documents (RBAC protected)

- GET /admin/consents/export (RBAC protected)

Rules:

- Server MUST validate doc_version against currently published versions.

- Accept requests MUST write to user_consents + consent_events atomically (transaction).

- If required consents are missing/outdated, API MUST return a clear error requiring re-consent.

212.7 Enforcement Points (Hard Requirements)

the Implementation Agent MUST enforce consent gating at:

- Login success redirect (if re-consent required, route to consent screen)

- Checkout / booking confirmation step (block if missing required consents)

- Any PII document upload step (passport/ID) (block if missing required consents)

212.8 Localization & Content Governance

- Legal pages MUST support English now; Arabic-ready (RTL-ready) later.

- Admin must be able to maintain separate content per language/version.

- If a requested language is unavailable, fallback to English with a warning label.

212.9 Final Acceptance Criteria for Chapter 212

Completion is NOT accepted unless:

- Privacy Policy and Terms of Use are live on Web and Mobile

- Admin can publish/version policies

- Consent is logged with evidence fields

- Re-consent is enforced when versions change

- Admin can view and export consent logs

END OF CHAPTER 212

CHAPTER 213 – PAYMENT, FINANCIAL COMPLIANCE & AUDIT-READY LEDGER

This chapter standardizes all payment flows, financial records, and compliance controls so that NOVAX TRAVEL is production-grade, auditable, and dispute-resistant. It is ADDITIVE and MUST be implemented end-to-end (Web, Mobile, Admin, Backend).

213.1 Payment Methods Scope (Initial + Future-Proof)

The system MUST support an extensible "Payment Method Registry" with:

A) INITIAL PRIMARY METHOD (Mandatory):

- Bank Transfer via Al Kuraimi (manual or semi-automated verification)

B) OPTIONAL / FUTURE METHODS (Supported by design, can be disabled by feature flag):

- Card gateway

- Mobile money

- Cash-in-office / cash agent

- Wallet-only checkout

Admin MUST be able to enable/disable each method per country, per agency, and per company.

213.2 Financial Ledger (Non-Negotiable)

the Implementation Agent MUST implement an immutable, audit-ready ledger:

Core principle:

- Every financial change MUST be recorded as a ledger entry.

- No silent updates of balances.

Minimum tables/entities:

1) financial_ledger_entries

- id, entry_uuid, entry_type

- related_entity_type (booking/request/wallet/invoice)

- related_entity_id

- currency, amount, direction (debit/credit)

- actor_type (user/agent/admin/system)

- actor_id

- created_at (UTC)

- metadata (JSONB)

- checksum / integrity hash

- reversal_of_entry_id (nullable)

2) wallet_balances (derived or stored with strict reconciliation)

- user_id/agency_id/company_id, currency, balance

Rules:

- Ledger entries MUST be append-only.

- Reversals MUST create new entries linked via reversal_of_entry_id.

- Daily reconciliation job MUST verify:

sum(credits) - sum(debits) = balance per wallet/account.

213.3 Bank Transfer Verification Workflow (Al Kuraimi)

The system MUST support verified bank transfer with evidence and status controls.

Workflow:

1) User selects "Al Kuraimi Bank Transfer"

2) System generates:

- payment_reference_code

- amount_due

- deadline

3) User uploads proof (receipt image / reference number)

4) Payment enters status: pending_verification

5) Admin/Finance verifies and sets:

- verified (success)

- rejected (invalid)

- needs_more_info (request resubmission)

6) On verified:

- ledger credit is created

- booking/request proceeds

Mandatory rules:

- Evidence must be stored securely (object storage) with access logging.

- Verification actions MUST be audited (who/when/why).

- Admin cannot mark verified without providing verification_reason.

- Expired deadlines MUST auto-expire to failed/expired with notification.

213.4 Refund, Cancellation, Chargeback & Dispute Policy (Mandatory)

The system MUST model the following:

A) Refund Types:

- Full refund

- Partial refund

- Credit to wallet

- Reversal of unverified payment

B) Refund Preconditions:

- Booking state must allow refund

- Refund must reference original ledger entries

C) Disputes:

- Create dispute case with timeline, evidence, notes, admin actions

- Dispute states: opened, under_review, resolved, rejected

D) Chargeback (for future card gateways):

- Must be representable even if gateway not enabled yet

- Must create ledger entries and lock certain balances until resolved

213.5 Invoicing & Receipts (Audit-Ready)

Admin MUST generate:

- Invoice for each confirmed booking/request (where applicable)

- Receipt for each verified payment

Invoices MUST include:

- invoice_number (unique, sequential per tenant/country)

- buyer identity (user/company/agency)

- tax fields (optional per country configuration)

- currency and FX rate reference (if multi-currency)

Receipts MUST include:

- payment_reference_code

- verification details (masked where needed)

- proof link (RBAC protected)

213.6 Multi-Currency Rules (Mandatory)

- Base currency MUST be configurable (default USD).

- Every ledger entry MUST store:

- transaction currency

- base currency equivalent

- fx_rate_used

- fx_source (admin/manual/provider)

- Admin MUST control exchange rates and effective dates.

213.7 RBAC & Segregation of Duties (Mandatory)

Financial permissions MUST be separated:

- finance.verify_payment

- finance.issue_refund

- finance.view_ledger

- finance.export_ledger

- finance.manage_exchange_rates

- finance.manage_invoice_sequences

Rules:

- A user who verifies a payment SHOULD NOT be the same user who issues a refund, unless Super Admin overrides (override must be logged).

213.8 Export & Audit Support (Mandatory)

Admin MUST be able to export:

- Ledger entries (CSV/JSON)

- Invoices and receipts (PDF/ZIP)

- Dispute cases with evidence references

Exports MUST be logged and restricted by RBAC.

213.9 Final Acceptance Criteria for Chapter 213

Completion is NOT accepted unless:

- Ledger is append-only with reversal mechanism

- Bank transfer workflow is fully implemented with evidence + audit

- Invoices/receipts are generated

- Refund/dispute workflow exists

- Exports work and are permission-protected

- Daily reconciliation job runs and reports status

END OF CHAPTER 213

CHAPTER 214 – RELEASE MANAGEMENT, APK SIGNING & APP DISTRIBUTION POLICY

This chapter ensures safe, controlled releases for Web/Admin/API and Mobile APK with strict ownership of signing keys and repeatable deployment practices. It is ADDITIVE and mandatory.

214.1 Versioning Strategy (Mandatory)

All components MUST follow semantic versioning:

- Backend: X.Y.Z

- Web: X.Y.Z

- Admin: X.Y.Z

- Mobile APK: X.Y.Z + build_number

Admin Panel MUST display currently deployed versions for each component.

214.2 Release Channels (Mandatory)

The system MUST support:

- DEV

- STAGING

- PRODUCTION

Rules:

- STAGING must be deployable independently of PRODUCTION.

- Domain cutover to production must happen only after staging verification (as per Chapter 210).

214.3 Mobile APK Signing & Keystore Ownership (Non-Negotiable)

- APK MUST be signed with a keystore.

- The keystore MUST be owned and controlled by the Owner.

- the Implementation Agent MUST NOT permanently store the keystore outside secure provider secret storage.

- If CI/CD needs the keystore:

- It must be stored as encrypted secrets in CI (or equivalent)

- Access must be restricted

- Rotation/backup guidance must be provided in the Owner Runbook (Chapter 211)

the Implementation Agent MUST deliver:

- A keystore handling plan (secure storage + backup instructions)

- A documented procedure to rebuild signed APK without losing signing identity

214.4 Build & Release Automation (Mandatory)

the Implementation Agent MUST implement CI/CD that can:

- Build and deploy Backend (Render)

- Build and deploy Web/Admin (Vercel)

- Build APK (Release)

- Publish APK artifacts to secure storage (Backblaze or equivalent)

- Generate release notes automatically from commits + changelog

Each release must create:

- release_id

- component versions

- deployment timestamps

- operator (system/admin)

- status (success/failure)

- rollback reference

214.5 OTA Updates & Forced Update Policy (Must Integrate Existing OTA)

If OTA system exists:

- Admin can mark a version as:

- optional update

- forced update (block app usage until updated)

- App must check update policy on startup and periodically.

Rules:

- Forced update MUST show:

- reason

- version required

- download link

- Admin can schedule forced updates.

214.6 Rollback Policy (Mandatory)

the Implementation Agent MUST support rollback for:

- Backend (redeploy previous stable build)

- Web/Admin (redeploy previous build)

- Mobile:

- cannot rollback installed APK, but must support forced update to a known stable version

Rollback must be documented and executable without coding by the Owner (through provider UI + runbook steps).

214.7 Release Governance & Approval Gates

- Production release MUST require an explicit admin approval step (RBAC protected).

- Any release that increases cost tiers must request Owner approval (Chapter 210 cost control).

214.8 Final Acceptance Criteria for Chapter 214

Completion is NOT accepted unless:

- Versioning is implemented and visible

- Staging and production channels exist

- APK signing is implemented and keystore ownership is guaranteed to the Owner

- CI/CD can build and publish artifacts

- OTA/forced update policy works (if enabled)

- Rollback procedure is delivered and tested on staging

END OF CHAPTER 214

CHAPTER 215 – ANALYTICS, PRODUCT METRICS & CONSENT-RESPECTING TELEMETRY

This chapter defines analytics governance, event schemas, dashboards, and strict privacy/consent enforcement aligned with Chapter 212. It is ADDITIVE and mandatory.

215.1 Core Consent Rule (Non-Negotiable)

The system MUST respect user consent:

- No analytics/telemetry beyond strictly necessary operations unless the user has explicitly consented (per Chapter 212).

- Marketing tracking MUST be separate consent from Terms/Privacy.

- If consent is withdrawn, analytics MUST stop immediately for that user.

215.2 Event Schema Governance (Mandatory)

the Implementation Agent MUST implement a standardized event schema:

event = {

event_name,

event_time_utc,

user_id (nullable for guest),

session_id,

source (web/mobile/admin),

tenant_id (agency/company),

locale,

metadata (JSONB)

}

Naming rules:

- snake_case event_name

- versioned schema: event_schema_version

215.3 Required Product Events (Minimum Set)

The system MUST emit (when consent allows):

A) Acquisition & Auth

- app_opened

- signup_started

- signup_completed

- login_success

- mfa_challenge_presented

- mfa_verified

B) Core Travel Funnel

- search_started (flights/hotels/cars/visas)

- search_results_viewed

- item_selected

- checkout_started

- payment_method_selected

- payment_proof_uploaded (bank transfer)

- booking_submitted

- booking_confirmed

- booking_failed

C) Admin Operations

- admin_login

- request_state_changed

- payment_verified

- refund_issued

- policy_published (legal docs)

D) Reliability

- api_error

- payment_verification_failed

- offline_sync_failed

- offline_sync_recovered

215.4 Privacy-by-Design & PII Restrictions (Mandatory)

- Events MUST NOT include PII:

passport numbers, full names, phone numbers, email contents, card-like data, credentials.

- Only pseudonymous IDs are allowed (user_id, request_id).

- Any debugging logs must be redacted.

215.5 Admin Analytics Dashboard (Mandatory)

Admin Panel MUST include dashboards:

- Conversion funnel (search -> checkout -> confirmed)

- Drop-off points and failure reasons

- Payment verification time metrics

- SLA compliance metrics

- Top routes, demand trends (aggregated)

- Agency/company budget usage impact on conversion (if enabled)

Dashboards must allow filtering:

- Date range

- Service type

- Tenant (agency/company)

- Channel (web/mobile)

- Country/city/route (aggregated)

215.6 Storage, Retention & Export

- Analytics data retention MUST be configurable (default: 12 months) and aligned with privacy policies.

- Admin can export aggregated analytics reports.

- Deletion requests (DSR) must remove or anonymize user-level analytics as per policy.

215.7 Feature Flags & Admin Control

Admin MUST be able to:

- Enable/disable analytics globally

- Enable/disable per channel (web/mobile)

- Enforce “consent required” gating

- Switch provider (internal storage vs external analytics) without code changes

215.8 Final Acceptance Criteria for Chapter 215

Completion is NOT accepted unless:

- Consent gating is enforced for analytics

- Standard event schema is implemented

- Required events exist (minimum set)

- PII is excluded from events

- Admin dashboards are live and filterable

- Retention/export controls exist and align with DSR requirements

END OF CHAPTER 215

# ========================================

# CHAPTER 216 – DOMAIN REGISTRAR OWNERSHIP, RENEWAL & ANTI-HIJACK POLICY

# ========================================

## 216.1 GOAL

Ensure novaxtravel.com is protected from expiry, hijack, or accidental transfer.

This chapter is operational and MUST be completed during go-live.

## 216.2 MANDATORY OWNER CONTROL

the Implementation Agent MUST confirm and document:

- Where the domain is registered (Registrar name).

- Owner has full admin access to the registrar account.

- Domain auto-renew is enabled (if available).

- WHOIS privacy enabled (if applicable).

- Registrar lock enabled (transfer lock / domain lock).

- Recovery email + 2FA enabled on registrar login.

## 216.3 RENEWAL & EXPIRY ALERTING

the Implementation Agent MUST configure at least two renewal alerts:

- 30 days before expiry

- 7 days before expiry

Alerts must be sent to Owner and an internal admin alert channel.

## 216.4 CHANGE CONTROL

Any action that affects domain routing MUST require explicit Owner confirmation:

- Nameserver changes

- DNS record bulk changes

- SSL/TLS mode changes

- Proxy toggling (Cloudflare orange/gray)

the Implementation Agent must log each planned change + rollback plan before execution.

# ========================================

# CHAPTER 217 – SECURITY HEADERS BASELINE + PUBLIC STATUS PAGE (LIGHTWEIGHT)

# ========================================

## 217.1 SECURITY HEADERS (MANDATORY)

the Implementation Agent MUST enable and validate baseline headers:

- HSTS (with safe rollout)

- X-Content-Type-Options: nosniff

- X-Frame-Options (or CSP frame-ancestors)

- Referrer-Policy

- Permissions-Policy

- Content-Security-Policy (CSP) with a safe default compatible with Next.js/Admin

Completion is NOT accepted unless the provider provides a verification report and confirms no breakage in Web/Admin/API.

## 217.2 PUBLIC STATUS PAGE (MINIMAL)

the Implementation Agent MUST provide one minimal status endpoint/page:

- /status (public) shows: "Operational / Degraded / Outage" + timestamp (no sensitive data).

- /health remains private/secured for internal checks (as already specified).

Status changes must be triggered automatically based on monitoring alerts.

## 217.3 OWNER RUNBOOK ADDITION

Owner Runbook must include:

- How to view status

- How to check DNS/SSL quickly

- How to rollback to last stable release

- Who receives alerts and where

CHAPTER 218 – ACCESSIBILITY, UX BASELINE & RTL-READINESS

This chapter ensures NOVAX TRAVEL provides a professional, inclusive user experience

and is prepared for Arabic/RTL expansion without breaking layouts. It is ADDITIVE and mandatory.

218.1 Accessibility Baseline (Web + Admin)

the Implementation Agent MUST implement baseline accessibility (WCAG-aligned best practices):

- Keyboard navigation for all interactive elements (menus, dialogs, forms).

- Visible focus states and consistent tab order.

- Proper labels for inputs (no unlabeled fields).

- ARIA roles for modals, alerts, and menus where needed.

- Error messages must be announced (screen-reader friendly).

- Color contrast and readable typography (no critical info by color alone).

- All images/icons used as buttons must have accessible labels.

Completion is NOT accepted unless:

- A basic accessibility checklist is verified across Web and Admin

- Critical flows (login, search, checkout, admin CRUD) pass keyboard-only navigation.

218.2 UX Baseline & Error Handling

The system MUST provide:

- Consistent loading states (skeletons/spinners) across all pages.

- Clear empty states (no data, no results).

- Friendly, actionable error messages (no raw stack traces).

- Standard error pages: 403, 404, 500 with recovery actions.

- Form validation with clear field-level messages.

- A unified notification/toast system.

218.3 RTL-Readiness (Arabic-Ready)

Even if Arabic content is not enabled initially, the system MUST be RTL-ready:

- UI layout must support direction switch (LTR/RTL) without UI breakage.

- Use logical CSS properties where possible and avoid hard-coded left/right.

- Ensure critical components (tables, forms, navbars) render correctly in RTL mode.

- Fonts must support Arabic characters.

Completion is NOT accepted unless:

- A test toggle for RTL mode exists in staging/admin settings

- Key screens render correctly in RTL mode.

218.4 Localization Rules

- English is primary now; Arabic later.

- All UI strings must be centralized (i18n).

- Date/time/currency formatting must be locale-aware.

- Admin can manage translations for custom content where applicable.

218.5 Acceptance Criteria

Completion is NOT accepted unless:

- Accessibility baseline is implemented

- Standard UX error/empty/loading states exist

- RTL readiness toggle exists and passes key-screen verification

END OF CHAPTER 218

CHAPTER 219 – SEO, INDEXING, PUBLIC PAGES & CONTENT POLICY

This chapter ensures NOVAX TRAVEL public web presence is discoverable, well-structured,

and has clear content governance. It is ADDITIVE and mandatory for public launch.

219.1 SEO Technical Requirements (Web)

the Implementation Agent MUST implement:

- Proper meta tags (title, description) per public page.

- OpenGraph and Twitter card metadata (optional but recommended).

- Canonical URLs for public pages.

- Clean URL routing and consistent slugs.

- Structured data (where applicable) without exposing sensitive info.

219.2 Indexing Controls

the Implementation Agent MUST provide:

- robots.txt with correct production rules

- sitemap.xml auto-generated and updated

- Noindex on sensitive pages:

- admin

- user account pages

- checkout pages

- internal dashboards

Completion is NOT accepted unless:

- robots.txt and sitemap.xml are reachable and valid

- noindex rules are correctly applied to private/sensitive routes.

219.3 Public System Pages (Mandatory)

Web MUST include:

- Home / Landing

- About

- Contact

- FAQ (basic)

- Terms of Use (from Chapter 212)

- Privacy Policy (from Chapter 212)

- Status page link (if implemented)

- Maintenance page (simple mode)

219.4 Content Policy & Governance

Admin MUST have a basic content governance module or settings:

- Manage FAQ entries

- Manage contact details (email/phone)

- Manage social links

- Control maintenance mode banner/message

- Publish/Unpublish content items

All changes MUST be audited.

219.5 Acceptance Criteria

Completion is NOT accepted unless:

- SEO meta structure exists

- robots.txt and sitemap.xml exist and validate

- Public pages exist and are editable where required

- Sensitive routes are protected from indexing

END OF CHAPTER 219

CHAPTER 220 – PERFORMANCE BUDGET, LOAD TARGETS & CACHING POLICY

This chapter defines measurable performance targets and required caching/CDN rules.

It is ADDITIVE and mandatory for production quality.

220.1 Performance Targets (Minimum)

the Implementation Agent MUST target:

API:

- p95 response time for core endpoints < 800ms under normal load

- error rate < 1% for core endpoints

Web/Admin:

- initial page load must be optimized with caching and code-splitting

- avoid blocking scripts and excessive bundle sizes

Mobile:

- offline-first screens must load without network

- sync must be resilient with backoff and batching

Targets must be documented in the final report.

220.2 Performance Budget (Mandatory)

the Implementation Agent MUST implement a performance budget:

- Control image sizes and formats (use modern formats where supported).

- Limit payload sizes for list endpoints with pagination.

- Use compression for API responses.

- Use caching headers for public assets.

- Avoid exposing heavy admin queries without pagination and filters.

220.3 Caching Strategy (Mandatory)

The system MUST define caching layers:

- CDN caching for static assets (via Vercel/Cloudflare)

- API caching for read-heavy endpoints where safe

- Server-side caching for lookups (airlines, cities, routes, settings)

- Client caching rules for mobile offline data

Rules:

- Cache invalidation must be defined for datasets and settings.

- Sensitive data MUST NOT be cached publicly.

220.4 Load Test & Verification (Minimum)

the Implementation Agent MUST execute a basic load test (staging) for:

- login

- search endpoints

- request creation

- admin list endpoints

Output:

- a short report with p95 latency and error rate

- recommended scaling actions (only with Owner approval per cost policy)

220.5 Acceptance Criteria

Completion is NOT accepted unless:

- Targets and budgets are defined and documented

- Caching strategy is implemented

- Basic load test report is delivered

END OF CHAPTER 220

CHAPTER 221 – SUPPORT OPERATIONS, TICKETING & CUSTOMER SERVICE SLA

This chapter ensures NOVAX TRAVEL can handle real customer support with traceable

tickets, SLA, and audit. It is ADDITIVE and mandatory for operational readiness.

221.1 Support Ticket System (Mandatory)

Admin Panel MUST include a Support Ticket module:

Ticket fields:

- ticket_id, user_id (nullable), channel (web/mobile/email), category, priority

- subject, description

- status (new, in_progress, waiting_user, resolved, closed)

- assigned_to (admin/agent)

- created_at, updated_at

- related_request_id / booking_id (optional)

- attachments (optional, stored securely)

221.2 SLA and Priority Rules

Priorities:

- P0 critical (payment or account lockout)

- P1 high (booking failure)

- P2 normal

- P3 low

SLA Targets:

- P0 first response within 30 minutes

- P1 first response within 2 hours

- P2 first response within 12 hours

- P3 first response within 24 hours

SLA breach must create admin alerts.

221.3 Templates & Macros (Mandatory)

Admin must have:

- reply templates (macros) per category

- internal notes vs customer-visible replies

- multi-language readiness (English now, Arabic later)

221.4 Audit & Export

All ticket actions must be logged:

- status changes

- assignments

- replies

- attachment access

Exports:

- ticket list export (CSV/JSON) with RBAC restrictions

221.5 Customer Visibility (Optional but Recommended)

Web/Mobile should provide a simple “My Support” page:

- user can open a ticket

- user can view status and replies

- user can upload requested documents

221.6 Acceptance Criteria

Completion is NOT accepted unless:

- Ticket module exists and works

- SLA rules and alerts exist

- Templates/macros exist

- Audit logging is enabled

- Export is available with RBAC

END OF CHAPTER 221

CHAPTER 222 – DATA QUALITY, MASTER DATA GOVERNANCE & APPROVAL WORKFLOWS

This chapter enforces high data quality and controlled governance for all master data

(e.g., Yemen governorates/cities/routes/airlines, global catalog data, pricing lookups).

It is ADDITIVE and strongly recommended for production stability.

222.1 Core Principles (Non-Negotiable)

- Master Data MUST be consistent, validated, and auditable.

- No silent edits: every change MUST be logged with actor + timestamp + reason.

- High-risk datasets MUST require approval before becoming active in production.

222.2 Master Data Categories (Minimum)

The system MUST treat the following as Master Data:

Yemen Domestic:

- governorates

- cities

- airports (if used)

- airlines (domestic carriers)

- domestic routes

- route schedules (if used)

- baggage rules (if configured)

Global/General:

- countries/cities (if enabled)

- hotel catalogs (if enabled)

- visa country requirements (if enabled)

- pricing rule dictionaries

- notification templates

- content items (FAQ, public pages)

222.3 Data Validation Rules (Mandatory)

the Implementation Agent MUST implement validation for master data:

- Uniqueness constraints:

- unique city per governorate by normalized name

- unique route per (origin, destination, airline) where applicable

- unique airline code (IATA/ICAO if used)

- Normalization:

- store a normalized_name field for duplicate detection

- consistent casing and trimming

- Referential integrity:

- routes must reference existing cities/airlines

- schedules must reference existing routes

- Safe deletion:

- prevent deleting master data if referenced by requests/bookings

- use soft-delete + archive state when needed

Admin UI MUST show validation errors clearly and block invalid saves.

222.4 Import/Export Governance (Mandatory)

Bulk imports MUST support:

- pre-import validation preview (dry-run)

- error report (row-level reasons)

- partial import rules (do not import invalid rows)

- rollback import (revert by import_batch_id)

Exports MUST be RBAC protected and audited.

222.5 Approval Workflow (Mandatory for High-Risk Data)

For high-risk datasets (routes, pricing dictionaries, airline rules, visa requirements):

- Draft → Pending Approval → Approved → Active

- Only “Active” is used by production flows.

Roles/Permissions (minimum):

- masterdata.edit_draft

- masterdata.submit_for_approval

- masterdata.approve

- masterdata.publish_activate

- masterdata.audit_view

Every approval action MUST store:

- approver_id

- approved_at

- approval_notes

- diff summary (what changed)

222.6 Change Log & Diffing (Mandatory)

the Implementation Agent MUST implement a change log for all master data:

- entity_type, entity_id

- action (create/update/archive/restore)

- before_snapshot (JSONB)

- after_snapshot (JSONB)

- actor_id, actor_type

- reason (required for update/archive)

- created_at (UTC)

Admin MUST display:

- version history

- who changed what

- ability to compare versions (diff view)

222.7 Acceptance Criteria

Completion is NOT accepted unless:

- Master data validation exists and blocks bad data

- Bulk import has dry-run + error reporting

- Approval workflow exists for high-risk datasets

- Change log and diff view exist in Admin

END OF CHAPTER 222

CHAPTER 223 – SENSITIVE DATA ACCESS COMPLIANCE, MASKING & ABNORMAL-ACCESS ALERTS

This chapter enforces strict compliance logging and protection for sensitive data such as:

passport/ID documents, bank transfer proofs, tickets, invoices, and any identity artifacts.

It is ADDITIVE and strongly recommended for production legality and trust.

223.1 Sensitive Data Definition (Mandatory)

Sensitive data includes:

- Passport / National ID images and numbers

- Visa documents

- Bank transfer receipts and references

- Tickets and booking confirmations containing PII

- Any uploaded files linked to user identity

223.2 Mandatory Access Logging (Non-Negotiable)

Any time sensitive data is:

- viewed

- downloaded

- exported

- printed

- shared via link

the system MUST record an immutable access log entry:

sensitive_access_logs:

- id

- actor_type (admin/agent/user/system)

- actor_id

- target_user_id (nullable)

- document_type (passport/id/receipt/ticket/visa/other)

- document_id or storage_key

- action (view/download/export)

- source (web/admin/mobile/api)

- ip_address

- device_id (nullable)

- user_agent (nullable)

- occurred_at (UTC)

- reason (required for admin/agent access)

- metadata (JSONB)

Rules:

- Admin/agent access MUST require a “reason” text field.

- Logs MUST be retained at least 7 years or per policy.

- Logs MUST be exportable only by the highest RBAC roles.

223.3 Masking & Redaction Policy (Mandatory)

The system MUST apply masking for sensitive fields:

- Show only partial document numbers (e.g., last 4 digits) in UI lists.

- Hide full numbers by default; require explicit "Reveal" action with audit log.

- Do not display raw PII in logs or analytics events.

- If screenshots/exports are generated, redact sensitive numbers unless explicitly required.

223.4 Secure Storage & Access Controls (Mandatory)

- All sensitive files MUST be stored in private object storage buckets.

- Access MUST be time-limited (signed URLs) and RBAC controlled.

- Public URLs are forbidden.

- Every access MUST pass authorization checks and produce an access log entry.

223.5 Abnormal Access Detection & Alerts (Mandatory)

the Implementation Agent MUST implement abnormal-access alerts, including:

- Too many sensitive document views/downloads by the same actor within time window

- Access outside normal business hours (configurable)

- Access to many different users’ documents by one actor

- Access from new/unrecognized device/IP for admin/agent roles

When triggered:

- Create a security_event record

- Notify Super Admin via alert channel

- Optionally auto-lock actor session pending review

223.6 Admin Compliance Dashboard (Mandatory)

Admin Panel MUST include:

- Sensitive Access Logs search/filter

- Export logs (RBAC protected)

- Abnormal access incidents list

- "Top viewers/downloaders" (internal compliance)

- Per-user document access timeline

223.7 Acceptance Criteria

Completion is NOT accepted unless:

- Sensitive data access is logged for view/download/export actions

- Masking/redaction is applied in UI and exports by default

- Signed URLs and private storage are enforced

- Abnormal access detection produces alerts and security events

- Compliance dashboard exists in Admin

END OF CHAPTER 223

CHAPTER 224 – BUSINESS CONTINUITY, SAFE MODE & OFFLINE OPERATIONS PLAYBOOK

This chapter defines how NOVAX TRAVEL continues operating during outages, weak

connectivity, provider downtime, or security events. It is ADDITIVE and mandatory

for resilient production operations, especially in low-connectivity environments.

224.1 Objectives (What This Chapter Guarantees)

- Continue critical operations during partial/total outages.

- Protect money and sensitive data during instability.

- Provide a clear “what to do now” playbook for Owner/Admin/Agents.

- Ensure all actions are logged and recoverable after service restoration.

224.2 Continuity Modes (Mandatory)

The system MUST support these operational modes:

A) NORMAL MODE

- All services online, full functionality.

B) DEGRADED MODE

- Non-critical functions limited (e.g., analytics, heavy reports, bulk exports).

C) SAFE MODE (PROTECTIVE MODE)

- High-risk actions blocked to prevent financial/data damage.

- Allowed actions are read-only or low-risk operations only.

D) OFFLINE MODE (MOBILE/AGENT)

- Mobile app works with local encrypted storage.

- Requests are created locally and queued for sync.

- No external calls required for basic intake.

224.3 Safe Mode Triggering Rules (Non-Negotiable)

the Implementation Agent MUST auto-trigger SAFE MODE when any of the following occurs:

- Database connectivity failures (Neon down / connection pool exhausted)

- Elevated error rates for core endpoints (threshold configurable)

- Payment verification subsystem unstable or suspected fraud spike

- Abnormal sensitive data access alerts (Chapter 223)

- Cloudflare/DNS misrouting detected

- Deployment in progress (optional safety window)

SAFE MODE MUST be:

- Visible in Admin "Status Center"

- Logged as a security_event with reason and timestamp

- Reversible only by authorized roles (RBAC) with audit reason

224.4 Allowed vs Blocked Actions in SAFE MODE

In SAFE MODE, the system MUST enforce:

ALLOWED (Low Risk):

- Login (with MFA)

- View existing requests/bookings

- View pricing rules (read-only)

- View audit logs / health dashboard

- Create support tickets

- Create draft requests (not confirm/charge)

BLOCKED (High Risk):

- Payment verification approvals

- Refund issuance

- Wallet balance manual adjustments

- Bulk imports/exports of sensitive data

- Publishing new pricing rules to production

- Admin schema changes / migrations

- Mass notifications

All blocked attempts must show a clear message and be logged.

224.5 Offline Operations Workflow (Agent/Mobile) (Mandatory)

When OFFLINE:

1) Agent can create a new request locally:

- traveler details (minimal required)

- route/service selection

- notes and attachments (queued)

2) Request is saved to local encrypted DB with:

- local_request_id

- created_at

- sync_status = pending

3) App shows the queue:

- pending, failed, synced

When connectivity returns:

1) Sync starts automatically with backoff + batching.

2) Conflicts resolved per Chapter 209 Offline Rules:

- server wins for master data

- merge non-conflicting fields

3) If upload fails:

- request remains pending, app shows retry option

4) Payment steps are NOT finalized offline unless explicitly allowed by policy

(default: payment verification requires online).

224.6 Manual Workarounds During Outage (Playbook)

If major outage occurs, staff must follow:

A) Intake Continuity

- Continue taking customer requests using Offline Mode on mobile.

- If mobile unavailable, use a simple paper/CSV intake template (admin can import later).

B) Financial Safety

- Do NOT approve payments manually inside system while SAFE MODE is active.

- Collect bank transfer references but mark as "Pending Verification".

C) Customer Communication

- Show a short outage banner on web (maintenance mode if needed).

- Inform customers: “Your booking is protected and will be processed once systems recover.”

D) Evidence Handling

- Attachments can be captured offline and uploaded later.

- Never share sensitive docs over public channels.

224.7 Recovery Plan (Return to Normal) (Mandatory)

When services are restored:

1) Verify core dependencies:

- Neon DB reachable

- Backend health /health OK

- Storage access OK

- DNS/SSL OK

2) Disable SAFE MODE only after:

- error rate normal for a defined stability window

- no ongoing abnormal access alerts

3) Process backlog:

- sync offline queues

- verify pending payments

- confirm bookings

4) Run post-recovery checks:

- ledger reconciliation (Chapter 213)

- sensitive access audit review (Chapter 223)

- incident report creation (if incident occurred)

224.8 Roles & Responsibilities (Owner/Admin/Agent)

Owner:

- Approves any paid upgrades or emergency provider changes (Chapter 210 cost control).

- Holds final authority for SAFE MODE override.

Super Admin:

- Enables/disables SAFE MODE with reason.

- Coordinates incident response and communication.

Finance Admin:

- Handles payment verification and refunds only after stability is confirmed.

Support Admin:

- Updates customer-facing messages and processes support tickets.

Agents:

- Use Offline Mode for request intake.

- Do not perform payment approvals.

224.9 Tools & Dashboards Required (Mandatory)

Admin Panel MUST include:

- Status Center (Normal/Degraded/Safe)

- System Health dashboard (/health summary)

- Offline Sync monitoring (queue stats, failures)

- Incident log (security_events)

- Backlog processing queue (pending_verification, pending_sync)

224.10 Acceptance Criteria for Chapter 224

Completion is NOT accepted unless:

- SAFE MODE exists with clear triggers, blocked actions, and audit logging

- Offline Mode creates queued requests and syncs reliably

- Admin has Status Center and backlog processing tools

- A recovery checklist is delivered in the Owner Runbook (Chapter 211)

END OF CHAPTER 224

CHAPTER 225 – THIRD-PARTY INTEGRATIONS GOVERNANCE, SAFE CONNECTORS & KILL SWITCH

This chapter defines how NOVAX TRAVEL integrates with third-party providers

(flights, hotels, payments, messaging, analytics) safely and operationally.

It prevents external integrations from breaking the system, leaking secrets,

or causing unexpected costs. It is ADDITIVE and mandatory for any external provider use.

225.1 Integration Scope (Examples, Not Limited)

This applies to any provider such as:

- Flight aggregators (e.g., Duffel, Travelpayouts)

- Hotel aggregators / bedbanks

- Payment gateways (future)

- SMS/Email providers

- Maps/geocoding (future)

- Fraud/verification tools

- Analytics tools (if enabled)

- Any webhook-based services

225.2 Core Principles (Non-Negotiable)

- Integrations MUST be modular and disable-able via feature flags.

- Secrets MUST never be stored in code or logs (env/secret manager only).

- External failures MUST NOT crash core operations; system must degrade gracefully.

- Every integration call MUST be observable (metrics + error logs + tracing IDs).

- Cost-impacting calls MUST be controlled (rate limits + quotas).

225.3 Integration Registry (Mandatory)

Admin Panel MUST include an "Integrations" module (Integration Registry) with:

For each integration:

- provider_name

- integration_type (flights/hotels/payments/notifications/other)

- status (disabled/enabled/testing/suspended)

- environment (staging/production)

- credentials_status (missing/valid/rotated/expired) (no secret values shown)

- base_url / endpoints (masked)

- webhook_urls (if any)

- last_health_check_at

- last_error_at

- quota_limits (daily/monthly/request rate)

- cost_guardrails (max_calls_per_minute, max_calls_per_day)

RBAC permissions:

- integrations.view

- integrations.configure

- integrations.enable_disable

- integrations.rotate_secrets

- integrations.view_logs

225.4 Integration Kill Switch (Mandatory)

The system MUST support an immediate "Kill Switch" per integration:

- Admin can disable an integration instantly.

- When disabled:

- all calls are blocked

- fallback behavior activates (see 225.5)

- a security_event is logged with who/why/when

- Kill Switch must be available in:

- Admin Integrations module

- Admin Status Center (quick toggle)

Completion is NOT accepted unless kill switch works in production.

225.5 Fallback Behaviors (Graceful Degradation) (Mandatory)

the Implementation Agent MUST implement clear fallback logic:

Flights:

- If provider unavailable:

- show "Temporarily unavailable" + allow manual request workflow

- do not block the entire app

Hotels/Cars/Visas:

- If provider unavailable:

- allow "Request quote" manual flow

- store request in pending_external_quote

Payments:

- If gateway unavailable:

- fallback to bank transfer (Al Kuraimi) if enabled

- block high-risk operations safely (SAFE MODE if necessary)

Notifications:

- If provider unavailable:

- queue messages and retry with backoff

- show admin warning

225.6 Standard Connector Pattern (Mandatory)

All integrations MUST be implemented as connectors with:

- timeouts and retries (with exponential backoff)

- circuit breaker (trip on repeated failures, then cool down)

- idempotency keys for booking/payment calls

- request/response schema validation

- consistent error mapping to internal error codes

- correlation_id for tracing

No connector may:

- log secrets

- store secrets

- bypass RBAC

225.7 Webhooks Governance (Mandatory)

If a provider uses webhooks:

- Webhook endpoints MUST verify signatures (HMAC or provider method).

- Use replay protection (nonce/timestamp window).

- Log webhook events:

- provider, event_type, received_at, status, correlation_id

- Provide an admin page to view webhook deliveries and retries.

225.8 Quotas, Rate Limits & Cost Guardrails (Mandatory)

For each integration, Admin MUST be able to set:

- max_calls_per_minute

- max_calls_per_day

- max_concurrent_requests

- optional cost ceiling estimates

When limits reached:

- throttle or block calls

- log a warning event

- optionally auto-disable integration (with notification)

Cost control MUST follow Chapter 210.15 (owner approval for paid changes).

225.9 Data Mapping & Reconciliation (Mandatory)

the Implementation Agent MUST define mapping rules:

- Provider objects (offers/bookings/hotels) map to internal models.

- Store provider_reference_id for reconciliation.

- Maintain an integration_audit table:

- internal_entity_id, provider_reference_id, provider_name

- request_payload_hash, response_payload_hash (redacted)

- status, timestamps

- Support "replay" of failed operations safely (idempotent).

225.10 Security Rules (Mandatory)

- Secrets stored only in provider env/secrets.

- Rotate secrets after deployment (Chapter 211.2).

- Access to integration configuration is restricted by RBAC.

- Any abnormal integration traffic triggers alerts (rate spikes, repeated failures).

- Sensitive data sent to providers must be minimized (data minimization principle).

225.11 Testing & Staging Requirements (Mandatory)

Before enabling any integration in production:

- Must be tested in staging first.

- Provide test report:

- success flows

- failure flows

- latency and error rates

- Provide rollback plan:

- disable via kill switch

- revert mapping changes if needed

225.12 Acceptance Criteria for Chapter 225

Completion is NOT accepted unless:

- Integrations module exists in Admin

- Kill switch works and is audited

- Fallback workflows work when providers fail

- Circuit breaker + idempotency implemented for key operations

- Webhooks are verified and logged

- Quotas/rate limits and cost guardrails are configurable

- Staging-first enablement is enforced

END OF CHAPTER 225

CHAPTER 226 – FINAL GO-LIVE CHECKLIST, EVIDENCE PACKAGE & OWNER SIGN-OFF

This chapter defines the FINAL “DONE” criteria for NOVAX TRAVEL. It prevents premature

completion claims and ensures real production readiness. It is ADDITIVE, mandatory, and

must be executed after deployment tasks are finished.

226.1 Core Rule (Non-Negotiable)

the Implementation Agent MUST NOT declare the project “COMPLETED” until:

1) All go-live checks in this chapter are executed successfully, AND

2) The Evidence Package is delivered, AND

3) The Owner explicitly confirms (Owner Sign-off) that novaxtravel.com is working.

226.2 Final Go-Live Checklist (Mandatory)

the Implementation Agent MUST execute and document the following checks:

A) DOMAIN & SSL (PUBLIC)

- novaxtravel.com opens the production Web successfully.

- www.novaxtravel.com opens the production Web successfully.

- SSL is valid with no browser warnings.

- Redirect policy is correct (http→https, www/non-www as configured).

B) ADMIN ACCESS (SECURE)

- Admin URL is reachable and protected.

- Super Admin can log in.

- Password change on first login is enforced.

- MFA is enabled/configured for admin roles (where required by policy).

- RBAC is verified (a limited role cannot access super-admin pages/endpoints).

C) API HEALTH & CORE DEPENDENCIES

- API production URL responds and passes /health checks.

- DB connectivity is confirmed (Neon).

- Storage connectivity is confirmed (Backblaze B2).

- Queue/worker status is healthy (if used).

- Error rate is within expected thresholds.

D) PAYMENTS (CURRENT MODE)

- Bank transfer (Al Kuraimi) flow works end-to-end:

- payment intent/reference created

- proof upload (if enabled) works

- verification workflow works

- receipt generation works

- Ledger reconciliation job runs and reports OK (Chapter 213).

E) EMAIL & NOTIFICATIONS

- OTP email delivery succeeds (real test delivered).

- SPF/DKIM/DMARC records are provided and validated (if applicable).

- Push notifications (Firebase/FCM) test succeeds (if enabled).

F) LEGAL & CONSENT (PUBLIC + LOGGED)

- Terms of Use page is live.

- Privacy Policy page is live.

- Consent capture is enforced and logged.

- Re-consent triggers when policy version changes (Chapter 212).

G) MONITORING, ALERTS & STATUS

- System Health dashboard exists in Admin.

- Alerts are configured for downtime/error spikes/DB failures.

- Status Center indicates correct operational state (Normal/Degraded/Safe) (Chapter 224).

H) BACKUPS & ROLLBACK

- Automated DB backups are enabled with retention confirmed.

- Rollback steps are documented and verified on staging:

- revert backend/web deploy to last stable build

- revert DNS changes if needed

- Secret rotation is completed and verified (Chapter 211).

I) SUPPORT OPERATIONS

- Support Ticket module works (create, assign, respond).

- SLA alerts are configured as required (Chapter 221).

226.3 Evidence Package (Mandatory Deliverables)

the Implementation Agent MUST deliver a single final Evidence Package that contains:

1) Production URLs:

- Web: https://novaxtravel.com + https://www.novaxtravel.com

- Admin: final admin URL

- API: final API URL

2) DNS Records (Exact Values):

- A/AAAA/CNAME for @, www, api (if used)

- Any required TXT records (SPF/DKIM/DMARC)

3) Credentials Handover:

- Super Admin credentials (temporary) + enforced password change

- Confirmation that no plaintext secrets are stored in code or docs

4) Deployment Report:

- Component versions (backend/web/admin/mobile)

- Deploy timestamps

- Provider resources created (Render/Vercel/Neon/B2/Cloudflare/Firebase)

- Monitoring/alerts status

5) Verification Results:

- /health outputs summary (no secrets)

- Email test proof

- FCM test proof (if enabled)

- Ledger reconciliation status

- Backup status + restore drill note (if executed)

6) Final ZIP:

- Source code

- Migrations/seeds

- OpenAPI spec

- Runbooks/operations docs

- Configuration templates (no secrets)

226.4 Owner Sign-off (Final Acceptance Gate)

the Implementation Agent MUST request explicit Owner sign-off with this question:

“Please confirm: When you open novaxtravel.com now, do you see the live NOVAX TRAVEL site working with valid SSL?”

Rules:

- If Owner says “NO”, the Implementation Agent MUST continue fixing until “YES”.

- Only after Owner says “YES”, the Implementation Agent may mark the mission as completed.

226.5 Final Completion Statement (Mandatory Format)

Only after Owner sign-off, the Implementation Agent must finalize with:

- “COMPLETED – GO-LIVE VERIFIED”

- Include production URLs

- Include where Evidence Package is located/downloadable

- Include a short “Next Steps” for routine operations

END OF CHAPTER 226

CHAPTER 227 – RELIABILITY, SELF-HEALING & OPERATIONS HARDENING ADDENDUM

227.1 Purpose

This chapter strengthens production reliability and operations by adding self-healing runbooks, queue/backlog controls, tamper-resistant operational logging, and provider-aligned recovery routines. It is ADDITIVE and must not conflict with cost-control requirements in Chapter 210.

227.2 Operational Runbooks (Mandatory)

the Implementation Agent MUST deliver step-by-step runbooks that a non-technical Owner can follow from provider dashboards (Render/Vercel/Neon/Cloudflare/Backblaze), including exact menu paths where applicable.

• Incident response runbook (SEV-0/1/2 classification, immediate actions, communication).

• Downtime triage runbook (DNS/SSL, API health, DB connectivity, storage access, queues).

• Queue backlog runbook (detect backlog, scale workers safely, retry policies, dead-letter handling).

• Email/OTP failure runbook (SMTP auth, DNS SPF/DKIM/DMARC checks, bounce handling).

• Restore runbook (DB restore to staging, verification, then controlled production recovery).

• Deployment rollback runbook (Backend/Web/Admin revert to last stable release).

227.3 Self-Healing Rules & Automation (Mandatory)

The system MUST implement safe self-healing behaviors with hard guardrails to prevent runaway costs.

• Circuit breakers and exponential backoff for unstable dependencies (DB, storage, external providers).

• Automatic SAFE MODE entry (Chapter 224) on sustained core dependency failures.

• Health-based restart strategy for workers/services (where supported) with capped retries.

• Any auto-scaling MUST be bounded and MUST request Owner approval before any paid tier change (Chapter 210.15).

227.4 Queue Backlog Controls (Mandatory if queues exist)

If the system uses background queues/workers, the Implementation Agent MUST implement:

• Backlog thresholds with alerts (warning/critical).

• Dead-letter queue (DLQ) or equivalent failure capture with admin visibility.

• Idempotent job design for payment and booking-critical operations.

• Admin tools to reprocess or cancel failed jobs with audit logging.

• Worker concurrency limits and rate limits to protect DB and third-party integrations.

227.5 Operational Logging Integrity & Retention (Mandatory)

Operational logs (security events, audit logs, sensitive access logs) MUST be retention-controlled and tamper-resistant.

• Audit logs and sensitive access logs must be retained per policy (Chapters 223 and 211) with export capability.

• Where supported, enable immutable storage for exported compliance logs (e.g., object lock / WORM-capable storage).

• All exports must be RBAC-protected and recorded (who/when/what/why).

227.6 Provider-Aligned Recovery Checklist (Mandatory)

the Implementation Agent MUST provide a short provider-aligned recovery checklist that maps each critical failure to actions:

• Neon DB failure: verify status, reconnect, restore to staging, then recover production; confirm migrations and reconciliation.

• Render backend failure: check deploy logs, restart service, rollback release, verify /health and critical APIs.

• Vercel web/admin failure: rollback deployment, verify routes, ensure admin access and no index exposure.

• Backblaze storage failure: verify credentials, signed URL generation, bucket policies; temporarily block uploads if needed.

• Cloudflare/DNS failure: verify records, SSL mode, proxy settings; rollback DNS to last known good state.

227.7 Final Acceptance Criteria for Chapter 227

Completion is NOT accepted unless:

• Runbooks are delivered (incident, backlog, email/OTP, restore, rollback).

• Alerts exist for error spikes, downtime, backlog thresholds, and abnormal access patterns.

• Self-healing rules are implemented with cost guardrails.

• Operational logging/export retention and integrity requirements are in place.

• Recovery checklist is provider-aligned and validated on staging.

END OF CHAPTER 227
