---
title: "تصميم التفعيل والوصف"
summary: "كتابة frontmatter ووصف triggering يجعل الوكيل يكتشف المهارة في اللحظة الصحيحة."
order: 3
durationLabel: "24 دقيقة"
type: "lesson"
isFreePreview: false
---

# تصميم التفعيل والوصف

في كثير من أنظمة الـ Skills، الوصف الموجود في الـ frontmatter ليس مجرد تعريف تسويقي، بل هو **الآلية الأولى التي يقرر بها الوكيل هل يستدعي المهارة أم لا**.

إذا كان هذا الوصف عامًا أكثر من اللازم، ستفشل المهارة في التفعيل. وإذا كان واسعًا أكثر من اللازم، ستبدأ بالتطفل على مهام ليست لها.

{% callout title="لا تكتب وصفًا جميلًا فقط" tone="warning" %}
اكتب وصفًا قابلًا للاكتشاف. يجب أن يشرح: ماذا تفعل المهارة، ومتى تستخدم، وما الإشارات الواقعية التي تجعلها الخيار الصحيح.
{% /callout %}

## ما الذي يجب أن يظهر في الوصف؟

1. نوع المهمة التي تتقنها المهارة.
2. السياقات أو العبارات التي تشير إلى الحاجة لها.
3. الأسماء أو الملفات أو الأنظمة أو المخرجات المرتبطة بها.
4. الحدود التي تميزها عن مهارات مجاورة.

## مثال ضعيف مقابل مثال قوي

{% accordion title="وصف ضعيف" open=true %}
`Skill تساعد في الوثائق.`

هذا الوصف لا يذكر نوع الوثائق، ولا متى تستخدم المهارة، ولا ما الذي يجعلها مختلفة عن مهارة كتابة عامة.
{% /accordion %}

{% accordion title="وصف أقوى" %}
`Use when the user wants to localize a repository README, add multilingual README variants, preserve GitHub-flavored Markdown structure, or maintain language selectors across README files.`

هنا أصبح لدينا مهمة واضحة، وسياق repo، ونطاق مخرجات، وإشارات تفعيل قابلة للملاحظة.
{% /accordion %}

## إشارات تفعيل قوية

- أسماء ملفات مثل `README.md` أو `CLAUDE.md` أو `Dockerfile`
- عبارات استخدام مثل "configure", "wire", "review this PR", "compress memory file"
- سياقات تقنية مثل Playwright أو PDF أو React أو packaging
- أنواع مخرجات محددة مثل sibling files أو benchmark أو localized docs

## كيف تمنع undertrigger وovertrigger؟

{% steps %}
{% step title="اكتب إشارات متعددة" hint="لا تعتمد على كلمة واحدة" %}
اجمع بين الفعل والسياق: مثل "translate README" مع "multilingual repo" ومع "language selector".
{% /step %}
{% step title="اذكر الحالات المتجاورة" %}
إذا كانت المهارة تنافس مهارة أخرى، وضّح لماذا هذه المهارة يجب أن تفوز في هذا السياق بالتحديد.
{% /step %}
{% step title="لا تجعل الوصف مقالة" %}
الوصف يجب أن يكون غنيًا بالإشارات لا بالتفاصيل الطويلة. التفاصيل التشغيلية مكانها داخل body أو المراجع.
{% /step %}
{% step title="اختبر الوصف بعيون المستخدم" %}
اسأل نفسك: هل طلب المستخدم العادي سيذكر هذه الإشارات فعلًا؟ أم أنني وصفت المهارة من الداخل فقط؟
{% /step %}
{% /steps %}

## Frontmatter عملي مقترح

```md
---
name: readme-i18n
description: Use when the user wants to translate a repository README, add multilingual README variants, preserve Markdown structure, or maintain language selectors across README files.
---
```

## قاعدة مهمة

ما يخص **"متى تُستخدم المهارة"** يجب أن يظهر مبكرًا وواضحًا. لا تدفنه في منتصف الملف بعد عشرات الأسطر من الشرح، لأن بعض الأنظمة تعتمد heavily على الحقول المبكرة في الاكتشاف.

{% reflection
  prompt="اكتب جملة واحدة تصف Skill في مشروعك بحيث تتضمن: ما الذي تفعله، ومتى تستخدم، وعلى أي نوع ملفات أو مهام."
  placeholder="مثال: Use when the user wants to..."
/%}

{% quickcheck
  prompt="أي وصف أقرب للتفعيل الجيد؟"
  options="مهارة تساعد في التطوير|مهارة تستخدم عند مراجعة pull requests وكتابة تعليقات كود مختصرة مع line references واضحة|مهارة ممتازة جدًا"
  answer="2"
  explanation="الوصف الجيد يحدد المهمة، والسياق، وشكل العمل المطلوب، بدل الاكتفاء بتعبير عام."
/%}

{% checkpoint title="ما الذي نحمله معنا؟" %}
- وصف المهارة هو جزء من نظام التفعيل، لا مجرد تعريف.
- اجمع بين الفعل والسياق ونوع الملف أو المخرج.
- اختبر دائمًا خطر undertrigger وovertrigger.
{% /checkpoint %}
