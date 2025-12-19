# NOVAX TRAVEL - استراتيجية المستودعات (Repository Strategy)

> **القرار:** Multi-Repo (NOT Monorepo)
> **التاريخ:** 2025-12-19

---

## 1. القرار القاطع

**نعتمد نمط Multi-Repo** لأسباب:
- فصل واضح للمسؤوليات
- CI/CD مستقل لكل خدمة
- صلاحيات مختلفة لكل فريق
- نشر مستقل بدون تأثير متبادل
- تاريخ Git نظيف لكل مكون

---

## 2. هيكل المستودعات

```
ytrextrvl/
├── novax_backend      # Laravel API (Render)
├── novax-admin        # Next.js Admin Panel (Vercel)
├── novax-travel       # Next.js Customer Web (Vercel)
├── novax-mobile       # Flutter Mobile App
└── novax-docs         # Documentation & Governance
```

---

## 3. قواعد الحدود

### Backend (`novax_backend`):
- ✅ Laravel PHP code
- ✅ Database migrations
- ✅ API routes
- ✅ Backend tests
- ❌ Frontend code
- ❌ Mobile code
- ❌ Admin UI

### Admin (`novax-admin`):
- ✅ Next.js admin dashboard
- ✅ Admin components
- ✅ Admin-specific assets
- ❌ Customer-facing code
- ❌ Backend logic
- ❌ Mobile code

### Web (`novax-travel`):
- ✅ Next.js customer website
- ✅ Customer components
- ✅ Public assets
- ❌ Admin code
- ❌ Backend logic
- ❌ Mobile code

### Mobile (`novax-mobile`):
- ✅ Flutter/Dart code
- ✅ Mobile assets
- ✅ Platform-specific configs
- ❌ Web code
- ❌ Backend logic

### Docs (`novax-docs`):
- ✅ Project documentation
- ✅ Architecture diagrams
- ✅ Governance files
- ✅ Checklists
- ❌ Application code

---

## 4. كيفية إضافة خدمات جديدة

### لإضافة خدمة جديدة:

1. **إنشاء مستودع جديد:**
   ```bash
   gh repo create ytrextrvl/novax-{service-name} --public
   ```

2. **إضافة الملفات الأساسية:**
   - README.md
   - .gitignore
   - DEPLOYMENT.md
   - .env.example

3. **تحديث التوثيق:**
   - تحديث REPO_INVENTORY.md
   - تحديث IMPLEMENTATION_ADDENDUM.md

4. **إعداد CI/CD:**
   - إضافة GitHub Actions workflow
   - ربط بـ Render/Vercel حسب النوع

---

## 5. قواعد التسمية

| النوع | النمط | مثال |
|-------|-------|------|
| Backend Service | `novax-{name}-api` | `novax-payments-api` |
| Frontend Web | `novax-{name}` | `novax-travel` |
| Admin Panel | `novax-{name}-admin` | `novax-admin` |
| Mobile App | `novax-{name}-mobile` | `novax-mobile` |
| Shared Library | `novax-{name}-lib` | `novax-ui-lib` |
| Documentation | `novax-docs` | `novax-docs` |

---

## 6. سياسة الفروع

```
main          # Production-ready code
├── feature/* # New features
├── fix/*     # Bug fixes
└── hotfix/*  # Emergency fixes
```

### قواعد:
- `main` محمي - يتطلب PR
- Feature branches تُحذف بعد الدمج
- Squash merge مفضل للحفاظ على تاريخ نظيف

---

> **آخر تحديث:** 2025-12-19
