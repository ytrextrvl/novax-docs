# خطة Phase 4 - الأمان والجاهزية

> **تاريخ الإنشاء:** 2025-12-20

---

## الهدف

تحقيق حالة "Audit-Ready" قبل النشر من خلال:
1. Security Baseline لكل مستودع
2. فحوص أمنية عبر GitHub Actions
3. Backend جاهز بواجهات /health و /ready و /version
4. OpenAPI Contract رسمي
5. Evidence Registry مركزي

---

## نطاق العمل

| المستودع | الإجراءات |
|----------|-----------|
| novax-docs | هيكل التوثيق الأمني |
| .github | Workflows أمنية مشتركة |
| novax_backend | Endpoints + OpenAPI + Security Baseline |
| novax-admin | Security Baseline + Headers |
| novax-travel | Security Baseline + Headers |
| novax-mobile | Security Baseline + Deps Audit |
| novax-infra | Threat Model + Incident Response |

---

## القيود

- ممنوع النشر (Render/Vercel)
- ممنوع إدخال أسرار في GitHub
- ممنوع تغييرات كبيرة
- العمل عبر Branches + PRs فقط

---

## معايير النجاح

| المعيار | الحالة |
|---------|--------|
| كل repo له SECURITY_BASELINE.md | ⏳ |
| Security workflows تعمل | ⏳ |
| Backend /health /ready /version | ⏳ |
| OpenAPI موجود | ⏳ |
| Evidence مكتمل | ⏳ |

---

> **آخر تحديث:** 2025-12-20
