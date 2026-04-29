---
title: "تحدي بناء Plugin كامل لـ Codex"
lessonSlug: "codex-plugin-capstone"
externalUrl: "https://developers.openai.com/codex/plugins/build"
repoUrl: "https://github.com/openai/codex"
---

# المطلوب

ابنِ Plugin عربيًا حقيقيًا لـ `Codex` يعالج workflow متكررًا في فريقك، ثم جهّزه بحيث يمكن تثبيته من marketplace محلي أو على مستوى repo.

## المطلوب داخل التحدي

- اختر use case حقيقي، مثل مراجعة الوثائق أو تلخيص التذاكر أو تجهيز checklists تنفيذية
- أنشئ `.codex-plugin/plugin.json` يحتوي على metadata واضحة
- أضف skill واحدة على الأقل داخل `skills/`
- أضف `marketplace.json` مناسبًا للتثبيت المحلي أو على مستوى repo
- أضف `.mcp.json` أو `.app.json` إذا كان use case يحتاجها فعلًا
- اختبر الإضافة في Codex وتأكد أنها تظهر وتُثبَّت وتُستدعى

## معايير النجاح

- اسم الإضافة ثابت وواضح بصيغة `kebab-case`
- manifest صحيح ومساراته relative وتبدأ بـ `./`
- skill قابلة للتفعيل ولها حدود واضحة
- marketplace يعرف مكان الإضافة وسياسات تثبيتها
- تجربة التثبيت والاستخدام موثقة ويمكن تكرارها من شخص آخر

## امتداد اختياري

حوّل الإضافة إلى Git-backed marketplace بحيث يستطيع فريقك إضافتها عبر:

```bash
codex plugin marketplace add owner/repo --ref main
```

ثم اختبر الترقية أو التحديث عند إصدار نسخة جديدة من Plugin.
