# Mukaeb Courses Repository

هذا المستودع مخصص لمحتوى الدورات الخاصة بمنصة مكعب أكاديمي.  
أي محتوى يوضع داخل `courses/` يمكن مزامنته إلى المنصة عبر GitHub + Convex.

## Repository Name Suggestion

الاسم المقترح لهذا المستودع على GitHub:

```text
mukaeb-courses
```

والصيغة الكاملة داخل GitHub تكون عادة:

```text
YOUR_ORG/mukaeb-courses
```

## What Is Included

هذا المستودع يحتوي الآن على محتوى جاهز داخل:

- `courses/build-your-own-blockchain/`
- `courses/agent-skills-best-practices/`

وكل دورة تتبع البنية التالية:

```text
courses/
  course-slug/
    course.md
    lessons/
    quizzes/
    challenges/
```

## Required Environment Variables

استخدم هذه المتغيرات في مشروع Convex الذي يشغل المنصة:

```env
MUKAEB_GITHUB_REPO=YOUR_ORG/mukaeb-courses
MUKAEB_GITHUB_BRANCH=main
MUKAEB_GITHUB_TOKEN=github_pat_xxxxxxxxxxxxxxxxxxxx
MUKAEB_GITHUB_WEBHOOK_SECRET=replace_with_a_long_random_secret
MUKAEB_ADMIN_EMAILS=you@example.com
MUKAEB_ADMIN_TOKEN_IDENTIFIERS=your-token-identifier
```

## Next Step

الخطوة التالية مباشرة هي:

1. أنشئ مستودع GitHub جديد باسم `mukaeb-courses`
2. اربط هذا المجلد به
3. ارفع المحتوى
4. ضع متغيرات البيئة في Convex
5. أضف GitHub webhook

## Quick Start

من داخل هذا المجلد نفّذ:

```powershell
git add .
git commit -m "Seed Mukaeb courses repository"
git branch -M main
git remote add origin https://github.com/YOUR_ORG/mukaeb-courses.git
git push -u origin main
```

## Convex Setup

بعد رفع المستودع إلى GitHub، أضف القيم التالية داخل بيئة Convex:

```env
MUKAEB_GITHUB_REPO=YOUR_ORG/mukaeb-courses
MUKAEB_GITHUB_BRANCH=main
MUKAEB_GITHUB_TOKEN=github_pat_xxxxxxxxxxxxxxxxxxxx
MUKAEB_GITHUB_WEBHOOK_SECRET=replace_with_a_long_random_secret
MUKAEB_ADMIN_EMAILS=you@example.com
```

إذا كنت تستخدم `tokenIdentifier` بدل البريد للمشرف:

```env
MUKAEB_ADMIN_TOKEN_IDENTIFIERS=your-token-identifier
```

## Webhook Setup

داخل GitHub:

1. افتح `Settings`
2. افتح `Webhooks`
3. اختر `Add webhook`
4. اجعل `Payload URL`:

```text
https://YOUR-CONVEX-DEPLOYMENT/github/webhook
```

5. اختر `application/json`
6. ضع نفس قيمة `MUKAEB_GITHUB_WEBHOOK_SECRET`
7. اختر `Just the push event`

## Generate A Webhook Secret

يمكنك توليد secret قوي بهذا الأمر:

```powershell
node -e "console.log(require('crypto').randomBytes(32).toString('base64url'))"
```

## Sync Test

لاختبار المزامنة:

1. عدّل أي ملف داخل `courses/`
2. نفّذ `git add .`
3. نفّذ `git commit -m "Update course content"`
4. نفّذ `git push`
5. افتح لوحة الإدارة داخل المنصة وراجع المسودات

## Notes

- المنصة تقرأ المحتوى من `courses/`
- أي دورة جديدة يجب أن تكون داخل مجلد مستقل
- ملف `course.md` يعرّف بيانات الدورة
- الدروس داخل `lessons/`
- الاختبارات داخل `quizzes/`
- التحديات داخل `challenges/`

## Included Files

- `README.md` هذا الدليل
- `.env.example` قالب المتغيرات
- `courses/` محتوى الدورات الجاهز
