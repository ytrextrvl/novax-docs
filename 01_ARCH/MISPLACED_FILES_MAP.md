# NOVAX TRAVEL - خريطة الملفات المُزاحة (Misplaced Files Map)

> **تاريخ الفحص:** 2025-12-19

---

## الملفات التي تحتاج نقل

| Source Repo/Path | Target Repo/Path | التبرير |
|------------------|------------------|---------|
| `novax-travel/public/downloads/novax-travel-release.apk` | GitHub Releases on `novax-mobile` | ملفات APK يجب أن تكون في Releases وليس في الكود |

---

## ملفات مفقودة يجب إنشاؤها

| Target Repo | الملف المفقود | الأولوية |
|-------------|---------------|----------|
| `novax-admin` | `.env.example` | CRITICAL |
| `novax-admin` | `DEPLOYMENT.md` | CRITICAL |
| `novax-admin` | `.github/workflows/deploy.yml` | IMPORTANT |
| `novax-travel` | `.env.example` | CRITICAL |
| `novax-travel` | `DEPLOYMENT.md` | CRITICAL |
| `novax-travel` | `.github/workflows/deploy.yml` | IMPORTANT |
| `novax-mobile` | `README.md` | CRITICAL |
| `novax-mobile` | `DEPLOYMENT.md` | CRITICAL |
| `novax-mobile` | `.github/workflows/build.yml` | IMPORTANT |
| `novax_backend` | `openapi.yaml` or Swagger | CRITICAL |
| `novax_backend` | `postman_collection.json` | IMPORTANT |

---

## ملاحظات

1. **APK في novax-travel:** الملف `novax-travel-release.apk` موجود داخل `public/downloads/` - هذا غير صحيح لأن:
   - يزيد حجم المستودع بلا داعٍ
   - يصعب تتبع الإصدارات
   - **الحل:** نقله إلى GitHub Releases في `novax-mobile`

2. **لا يوجد محتوى مختلط آخر:** باقي المستودعات نظيفة من حيث الحدود

---

> **آخر تحديث:** 2025-12-19
