# NOVAX TRAVEL - خطة الفصل الآمن (Safe Split Plan)

> **تاريخ الإنشاء:** 2025-12-19
> **الهدف:** الحفاظ على تاريخ Git عند نقل الملفات

---

## الحالة الحالية

**لا يوجد فصل كبير مطلوب** - المستودعات الأربعة منظمة بشكل جيد.

الإجراء الوحيد المطلوب: نقل APK من `novax-travel` إلى GitHub Releases.

---

## إجراء نقل APK

### الطريقة المختارة: GitHub Releases (بدون git subtree)

**السبب:** ملف APK هو artifact وليس كود مصدري، لذا لا يحتاج الحفاظ على تاريخ Git.

### الخطوات:

```bash
# 1. نسخ APK محلياً
cp novax-travel/public/downloads/novax-travel-release.apk ./

# 2. إنشاء Release على novax-mobile
gh release create v1.0.0 \
  --repo ytrextrvl/novax-mobile \
  --title "NOVAX Travel v1.0.0" \
  --notes "Initial release" \
  ./novax-travel-release.apk

# 3. حذف APK من novax-travel
cd novax-travel
git rm public/downloads/novax-travel-release.apk
git commit -m "chore: move APK to GitHub Releases"
git push origin main

# 4. تحديث DownloadApkButton.tsx للإشارة إلى Release URL
```

### خطة الرجوع (Rollback):

```bash
# إذا حدث خطأ، استعادة الملف:
git checkout HEAD~1 -- public/downloads/novax-travel-release.apk
git commit -m "revert: restore APK file"
git push origin main
```

---

## خطط احتياطية (للمستقبل)

### Option A: git subtree (مفضل للكود)

```bash
# لفصل مجلد إلى مستودع جديد مع الحفاظ على التاريخ
git subtree split -P path/to/folder -b new-branch
cd /path/to/new-repo
git pull /path/to/original-repo new-branch
```

**المخاطر:**
- قد يفشل مع مسارات معقدة
- يتطلب تنظيف يدوي

**خطة الرجوع:**
- المستودع الأصلي لا يتأثر
- حذف المستودع الجديد إذا فشل

### Option B: git filter-repo (للحالات المعقدة)

```bash
# تثبيت الأداة
pip install git-filter-repo

# فصل مجلد
git filter-repo --path path/to/folder --path-rename path/to/folder/:
```

**المخاطر:**
- يعيد كتابة التاريخ بالكامل
- يتطلب force push

**خطة الرجوع:**
- الاحتفاظ بنسخة من المستودع قبل التنفيذ:
  ```bash
  git clone --mirror original-repo backup-repo
  ```

---

## ملخص القرارات

| الإجراء | الطريقة | الحالة |
|---------|---------|--------|
| نقل APK | GitHub Releases | ⏳ مؤجل لـ Phase 2+ |
| فصل كود | غير مطلوب | ✅ |
| دمج مستودعات | ممنوع (Multi-Repo) | ✅ |

---

> **آخر تحديث:** 2025-12-19
