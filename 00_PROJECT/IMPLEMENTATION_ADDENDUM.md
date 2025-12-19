# NOVAX TRAVEL - ملحق التنفيذ (Implementation Addendum)

> **المصدر:** NOVAX_TRAVEL_Project_Description_AR.docx  
> **التاريخ:** 2025-12-19  
> **الغرض:** تحويل وثيقة المشروع إلى Checklist تنفيذية قابلة للقياس

---

## 1. حدود المستودعات المطلوبة (Repository Boundaries)

| المستودع | النوع | الغرض | الحالة |
|----------|-------|-------|--------|
| `novax_backend` | Backend API | Laravel + PostgreSQL + JWT - خدمات API الخلفية | ✅ موجود |
| `novax-admin` | Admin Panel | Next.js - لوحة تحكم الإدارة | ✅ موجود |
| `novax-travel` | Customer Web | Next.js - موقع العملاء | ✅ موجود |
| `novax-mobile` | Mobile App | Flutter - تطبيق الجوال | ✅ موجود |
| `novax-docs` | Documentation | التوثيق والحوكمة | ✅ تم إنشاؤه |

### قواعد الحدود:
- **ممنوع** خلط كود Backend مع Frontend
- **ممنوع** وضع ملفات Mobile داخل Web
- **ممنوع** وضع Infra configs داخل كود التطبيق
- كل مستودع مستقل بـ CI/CD خاص به

---

## 2. Enterprise Docs Pack المطلوب لكل Repo

### Backend (`novax_backend`):
| الملف | الحالة | ملاحظات |
|-------|--------|---------|
| README.md | ✅ موجود | |
| DEPLOYMENT.md | ✅ موجود | |
| ENV_VARIABLES_REFERENCE.md | ✅ موجود | |
| ROLLBACK.md | ✅ موجود | |
| SECURITY.md | ✅ موجود | |
| ADMIN_OPERATIONS_GUIDE.md | ✅ موجود | |
| OpenAPI/Swagger | ❌ مفقود | CRITICAL |
| Postman Collection | ❌ مفقود | IMPORTANT |

### Admin (`novax-admin`):
| الملف | الحالة | ملاحظات |
|-------|--------|---------|
| README.md | ✅ موجود | |
| DEPLOYMENT.md | ❌ مفقود | CRITICAL |
| .env.example | ❌ مفقود | CRITICAL |

### Web (`novax-travel`):
| الملف | الحالة | ملاحظات |
|-------|--------|---------|
| README.md | ✅ موجود | |
| DEPLOYMENT.md | ❌ مفقود | CRITICAL |
| .env.example | ❌ مفقود | CRITICAL |

### Mobile (`novax-mobile`):
| الملف | الحالة | ملاحظات |
|-------|--------|---------|
| README.md | ❌ مفقود | CRITICAL |
| DEPLOYMENT.md | ❌ مفقود | CRITICAL |
| Build Guide | ❌ مفقود | CRITICAL |

---

## 3. معايير Evidence و Definition of Done

### A) Live URLs المطلوبة:
| URL | الغرض | الحالة |
|-----|-------|--------|
| https://novaxtravel.com | موقع العملاء | ⏳ غير منشور |
| https://www.novaxtravel.com | موقع العملاء (www) | ⏳ غير منشور |
| https://api.novaxtravel.com/health | Backend Health | ⏳ غير منشور |
| https://admin.novaxtravel.com | لوحة الإدارة | ⏳ غير منشور |

### B) إثبات النشر الخارجي:
- [ ] Render service(s) created and running
- [ ] Vercel projects created and linked to domain
- [ ] Neon DB migrated + seeded
- [ ] Cloudflare DNS + Full (Strict) SSL + basic WAF/rate limits enabled
- [ ] Backblaze buckets integrated via signed URLs
- [ ] Firebase FCM configured

### C) حزمة التسليم النهائية:
- [ ] DEPLOYMENT.md (exact steps + architecture)
- [ ] ENV_VARIABLES_REFERENCE.md
- [ ] ROLLBACK.md
- [ ] ADMIN_OPERATIONS_GUIDE.md (non-technical)
- [ ] SECURITY.md
- [ ] API (OpenAPI/Swagger) + Postman collection

---

## 4. سياسة الأسرار + آلية منع التسريب

### القواعد الأساسية:
1. **ممنوع** تخزين الأسرار داخل الكود أو ملفات ZIP
2. **ممنوع** commit لملفات `.env` الحقيقية
3. الأسرار **فقط** في:
   - Render Environment Variables
   - Vercel Environment Variables
   - GitHub Secrets
   - Cloudflare Secrets

### ملفات `.gitignore` المطلوبة:
```
.env
.env.local
.env.production
*.pem
*.key
```

### PR Checks المطلوبة:
- [ ] Secret scanning enabled on all repos
- [ ] Pre-commit hooks for secret detection
- [ ] Branch protection rules on `main`

---

## 5. المزودون الثابتون (Fixed Providers)

| الخدمة | المزود | ملاحظات |
|--------|--------|---------|
| Backend Hosting | Render | **ممنوع** استخدام Railway |
| Web + Admin | Vercel | |
| Database | Neon (PostgreSQL) | |
| DNS/SSL/WAF | Cloudflare | Full (Strict) SSL |
| Storage | Backblaze B2 | S3-compatible, signed URLs only |
| Push Notifications | Firebase FCM | |
| Domain/SMTP | Hostinger | |

---

## 6. النطاقات المطلوبة

| النطاق | الغرض |
|--------|-------|
| novaxtravel.com | الرئيسي |
| www.novaxtravel.com | إعادة توجيه |
| api.novaxtravel.com | Backend API |
| admin.novaxtravel.com | لوحة الإدارة |

---

## 7. نموذج المصادقة (Owner-Assisted Authentication)

المالك يقوم **فقط** بـ:
- تسجيل الدخول لحساباته
- الموافقة على OAuth prompts
- الموافقة على MFA/2FA
- قبول الدعوات
- (إذا لزم الأمر) لصق tokens لمرة واحدة

فريق التنفيذ يقوم بـ:
- الإعداد والتهيئة
- الربط والنشر
- CI/CD
- Migrations
- SSL/WAF
- المراقبة والتحقق النهائي

---

> **آخر تحديث:** 2025-12-19
