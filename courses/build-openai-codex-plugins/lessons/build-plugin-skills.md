---
title: "كيف تبني Skills جيدة داخل الإضافة؟"
summary: "كتابة `SKILL.md` داخل Plugin بحيث تكون قابلة للتفعيل، قصيرة السياق، وواضحة الحدود."
order: 3
durationLabel: "28 دقيقة"
type: "lesson"
isFreePreview: false
---

# كيف تبني Skills جيدة داخل الإضافة؟

إذا كان الـ Plugin هو حزمة التوزيع، فالـ **Skill** غالبًا هي قلب القيمة الفعلية. وثائق Codex تشرح أن skills هي صيغة authoring القابلة لإعادة الاستخدام، وأن Codex لا يحمّل النص الكامل لـ `SKILL.md` إلا عندما يقرر استخدام skill فعلًا.

{% callout title="لماذا هذا مهم؟" tone="tip" %}
هذا يعني أن skill الجيدة ليست فقط تعليمات صحيحة، بل أيضًا تعليمات يمكن اكتشافها من وصف قصير وواضح دون أن تستهلك السياق من البداية.
{% /callout %}

## كيف يختار Codex skill؟

بحسب الوثائق:

1. **تفعيل صريح**: عندما تذكر skill بالاسم.
2. **تفعيل ضمني**: عندما يطابق الطلب وصف skill.

ولهذا السبب يجب أن يكون حقل `description`:

- واضحًا
- محدد النطاق
- غنيًا بكلمات trigger حقيقية

## شكل skill داخل الإضافة

```bash
my-plugin/
  skills/
    openai-docs-review/
      SKILL.md
```

ومثال بسيط:

```yaml
---
name: openai-docs-review
description: Use when comparing two OpenAI docs pages, extracting implementation differences, or preparing a migration checklist.
---
```

```markdown
1. Read the referenced docs first.
2. Extract concrete changes only.
3. Separate stable guidance from volatile guidance.
4. Produce a concise implementation checklist.
```

## ما الذي يجعل skill قابلة للتفعيل فعلًا؟

{% steps %}
{% step title="صف trigger بدل كتابة شعار" hint="أهم نقطة" %}
لا تكتب وصفًا مثل "مفيد للبحث". اكتب وصفًا مثل "Use when comparing two OpenAI docs pages or creating an API migration checklist".
{% /step %}
{% step title="ضع حدودًا صريحة" %}
اشرح متى لا يجب استخدام skill حتى لا تتداخل مع skills أخرى أو مع السلوك العام.
{% /step %}
{% step title="صمّم workflow قابلاً للتحقق" %}
إذا لم تستطع التحقق من ناتج الخطوات، فالأرجح أن skill لا تزال عامة أكثر من اللازم.
{% /step %}
{% step title="استفد من progressive disclosure" %}
ضع summary ذكيًا في الـ metadata، واترك التفاصيل الثقيلة داخل `SKILL.md` نفسه.
{% /step %}
{% /steps %}

## أين تحفظ skills إذا لم تكن داخل Plugin؟

الوثائق الحالية تذكر أن Codex يقرأ skills من:

- `$CWD/.agents/skills`
- مجلدات أعلى داخل نفس repo
- `$REPO_ROOT/.agents/skills`
- `$HOME/.agents/skills`
- طبقات إدارية أو نظامية

لكن عندما تريد **توزيع skill خارج repo واحد** أو ربطها مع app أو MCP، فالوثائق توصي بالانتقال إلى Plugin.

## مثال عملي: skill داخل Plugin للبحث في وثائق OpenAI

```yaml
---
name: openai-plugin-architect
description: Use when designing Codex plugins that bundle skills, MCP servers, or OpenAI-related implementation guidance.
---
```

```markdown
## Purpose
Help the user design Codex plugins with accurate file structure and safe rollout steps.

## Use this skill when
- the task mentions Codex plugins
- the task mentions .codex-plugin/plugin.json
- the task needs marketplace.json or MCP wiring

## Do not use this skill when
- the user is asking about ChatGPT app monetization only
- the task is generic web development unrelated to Codex plugins

## Workflow
1. Confirm whether the task is about plugin authoring or app authoring.
2. Read the manifest and marketplace context.
3. Produce the minimum valid structure first.
4. Add optional integrations only when they serve the use case.
```

{% reflection
  prompt="إذا أنشأت skill داخل Plugin لفريقك، ما الجملة التي ستجعل Codex يلتقطها ضمنيًا من أول مرة؟"
  placeholder="اكتب سطر description واضحًا وقابلًا للملاحظة."
/%}

{% quickcheck
  prompt="ما سبب أهمية description المختصر والواضح في skill؟"
  options="لأنه بديل عن كل التعليمات|لأنه يساعد Codex على التفعيل الضمني دون تحميل المحتوى الكامل مبكرًا|لأنه يحسن لون البطاقة فقط"
  answer="2"
  explanation="Codex يبدأ من اسم skill ووصفها ومسارها، ثم يحمّل المحتوى الكامل لاحقًا عند الحاجة."
/%}

{% checkpoint title="قاعدة بناء skill داخل Plugin" %}
- اجعل الوصف قابلاً للملاحظة
- اكتب حدودًا تمنع التفعيل الخاطئ
- حافظ على workflow واضح وقابل للتحقق
- انتقل إلى Plugin عندما تريد توزيع skill لا مجرد تأليفها محليًا
{% /checkpoint %}
