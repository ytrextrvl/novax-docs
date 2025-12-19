# NOVAX TRAVEL - جرد المستودعات (Repository Inventory)

> **تاريخ الفحص:** 2025-12-19
> **عدد المستودعات:** 5

---

## جدول الجرد الشامل

| Repo | Type Guess | Tech Evidence | Buildability | Deploy Evidence | Secret Risk | Mixed Content | Recommended Target |
|------|------------|---------------|--------------|-----------------|-------------|---------------|-------------------|
| `novax_backend` | Backend API | Laravel 10, PHP 8.2, JWT, PostgreSQL | ✅ PASS - composer.json valid | CI/CD exists (laravel-deploy.yml) | ⚠️ LOW - .env.example only | ❌ Clean | Keep as-is |
| `novax-admin` | Admin Panel | Next.js 16, React 19, TypeScript, Tailwind | ✅ PASS - package.json valid | ❌ No CI/CD | ✅ NONE | ❌ Clean | Keep as-is |
| `novax-travel` | Customer Web | Next.js 13, React 18, TypeScript, Tailwind | ✅ PASS - package.json valid | ❌ No CI/CD | ✅ NONE | ⚠️ APK file present | Move APK to releases |
| `novax-mobile` | Mobile App | Flutter 3.x, Dart | ⚠️ PARTIAL - minimal structure | ❌ No CI/CD | ✅ NONE | ❌ Clean | Needs expansion |
| `novax-docs` | Documentation | Markdown | N/A | N/A | ✅ NONE | ❌ Clean | New - governance hub |

---

## تفاصيل كل مستودع

### 1. novax_backend

**التقنيات:**
- Laravel 10.x
- PHP 8.2
- PostgreSQL (via Neon)
- JWT Auth (tymon/jwt-auth)
- Spatie Permission & Activity Log
- Google 2FA

**الملفات الرئيسية:**
```
├── app/
│   ├── Http/Controllers/
│   │   ├── AuthController.php
│   │   ├── FlightsController.php
│   │   ├── RequestsController.php
│   │   ├── PricingController.php
│   │   ├── AgenciesController.php
│   │   ├── WalletController.php
│   │   └── Admin/
│   │       ├── UsersController.php
│   │       └── AuditController.php
│   └── Models/
│       ├── User.php
│       ├── Agency.php
│       ├── Flight.php
│       ├── City.php
│       ├── Governorate.php
│       └── ...
├── database/migrations/ (6 files)
├── routes/api.php
├── Dockerfile
└── .github/workflows/laravel-deploy.yml
```

**Health Endpoint:** ✅ `/api/health` returns `{"ok": true}`

**قابلية البناء:** ✅ PASS
- composer.json صالح
- Dependencies محددة
- Dockerfile موجود

---

### 2. novax-admin

**التقنيات:**
- Next.js 16.0.10
- React 19.2.3
- TypeScript 5.9.3
- Tailwind CSS 4.1.18
- Axios

**الملفات الرئيسية:**
```
├── app/
│   ├── layout.tsx
│   ├── page.tsx
│   └── dashboard/
│       ├── page.tsx
│       ├── settings/page.tsx
│       └── team/page.tsx
├── components/
│   ├── Login.tsx
│   └── dashboard/
│       ├── Sidebar.tsx
│       ├── TopBar.tsx
│       └── AICopilot.tsx
└── lib/axios.ts
```

**API Base URL:** `https://api.novaxtravel.com/api`

**قابلية البناء:** ✅ PASS
- package.json صالح
- Scripts: dev, build, start, lint

---

### 3. novax-travel

**التقنيات:**
- Next.js 13.4.19
- React 18.3.1
- TypeScript 5.9.3
- Tailwind CSS 4.1.18
- Axios

**الملفات الرئيسية:**
```
├── app/
│   ├── layout.tsx
│   ├── page.tsx
│   └── dashboard/page.tsx
├── components/
│   ├── Login.tsx
│   ├── CustomerAIChat.tsx
│   └── DownloadApkButton.tsx
├── public/
│   └── downloads/novax-travel-release.apk  ⚠️
└── lib/axios.ts
```

**ملاحظة:** يحتوي على APK file - يجب نقله لـ GitHub Releases

**قابلية البناء:** ✅ PASS

---

### 4. novax-mobile

**التقنيات:**
- Flutter 3.x
- Dart SDK >=3.0.0 <4.0.0

**الملفات الرئيسية:**
```
├── lib/
│   ├── main.dart
│   ├── screens/home_screen.dart
│   └── theme/novax_theme.dart
└── pubspec.yaml
```

**قابلية البناء:** ⚠️ PARTIAL
- هيكل أساسي فقط
- يحتاج توسيع كبير

---

### 5. novax-docs (جديد)

**الغرض:** مركز التوثيق والحوكمة

**الهيكل المخطط:**
```
├── 00_PROJECT/
│   ├── IMPLEMENTATION_ADDENDUM.md
│   ├── REPO_INVENTORY.md
│   └── REPO_STRATEGY.md
├── 01_ARCH/
│   ├── MISPLACED_FILES_MAP.md
│   └── SAFE_SPLIT_PLAN.md
└── CHECKLIST.md
```

---

## ملخص المخاطر

| المستودع | مخاطر الأسرار | محتوى مختلط | CI/CD |
|----------|---------------|-------------|-------|
| novax_backend | ⚠️ LOW | ❌ | ✅ |
| novax-admin | ✅ NONE | ❌ | ❌ |
| novax-travel | ✅ NONE | ⚠️ APK | ❌ |
| novax-mobile | ✅ NONE | ❌ | ❌ |
| novax-docs | ✅ NONE | ❌ | N/A |

---

> **آخر تحديث:** 2025-12-19
