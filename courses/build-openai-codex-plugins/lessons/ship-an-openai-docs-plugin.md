---
title: "ورشة عملية: ابنِ Plugin لوثائق OpenAI"
summary: "تطبيق كامل على Plugin عربي يضم skill للبحث في وثائق OpenAI مع Marketplace محلي وخطوات اختبار واضحة."
order: 8
durationLabel: "42 دقيقة"
type: "lesson"
isFreePreview: false
---

# ورشة عملية: ابنِ Plugin لوثائق OpenAI

في هذا الدرس سنجمع ما سبق في مثال واحد عملي: Plugin اسمه:

```bash
openai-docs-workshop
```

هدفه أن يمنح `Codex` workflow عربيًا منظمًا للتعامل مع وثائق OpenAI ومقارنتها وإنتاج checklists تنفيذية.

{% video
  title="تعرف على استخدامات Codex الحالية"
  src="https://openai.com/index/introducing-the-codex-app/"
  caption="إطلاق Codex app من OpenAI يوضح كيف أصبحت skills والـ workflows والتوزيع جزءًا من التجربة اليومية."
/%}

## الخطوة 1: أنشئ هيكل الإضافة

```bash
openai-docs-workshop/
  .codex-plugin/
    plugin.json
  skills/
    openai-docs-review/
      SKILL.md
  .mcp.json
  assets/
```

## الخطوة 2: اكتب `plugin.json`

```json
{
  "name": "openai-docs-workshop",
  "version": "0.1.0",
  "description": "Arabic workflows for OpenAI docs research and implementation planning.",
  "skills": "./skills/",
  "mcpServers": "./.mcp.json",
  "interface": {
    "displayName": "OpenAI Docs Workshop",
    "shortDescription": "Arabic OpenAI docs workflows for Codex",
    "longDescription": "Research, compare, and turn OpenAI docs into implementation checklists.",
    "developerName": "Mukaeb Academy",
    "category": "Productivity",
    "capabilities": ["Read", "Write"],
    "websiteURL": "https://example.com",
    "privacyPolicyURL": "https://example.com/privacy",
    "termsOfServiceURL": "https://example.com/terms",
    "defaultPrompt": [
      "Use OpenAI Docs Workshop to compare two OpenAI docs pages.",
      "Use OpenAI Docs Workshop to prepare an implementation checklist."
    ],
    "brandColor": "#10A37F"
  }
}
```

## الخطوة 3: اكتب skill عربية عملية

```yaml
---
name: openai-docs-review
description: Use when the user needs OpenAI docs comparison, migration notes, or implementation checklists in Arabic.
---
```

```markdown
## Workflow
1. Read the relevant docs first.
2. Separate stable facts from time-sensitive guidance.
3. Extract only decisions that affect implementation.
4. Produce a concise Arabic checklist.
```

## الخطوة 4: أضف `.mcp.json`

```json
{
  "mcpServers": {
    "openaiDeveloperDocs": {
      "transport": "streamable_http",
      "url": "https://developers.openai.com/mcp"
    }
  }
}
```

## الخطوة 5: أضف Marketplace محليًا

```json
{
  "name": "academy-local-plugins",
  "interface": {
    "displayName": "Academy Local Plugins"
  },
  "plugins": [
    {
      "name": "openai-docs-workshop",
      "source": {
        "source": "local",
        "path": "./plugins/openai-docs-workshop"
      },
      "policy": {
        "installation": "AVAILABLE",
        "authentication": "ON_USE"
      },
      "category": "Productivity"
    }
  ]
}
```

## الخطوة 6: ثبّت واختبر

{% steps %}
{% step title="انسخ الإضافة إلى المسار الذي يشير إليه marketplace" %}
مثل `./plugins/openai-docs-workshop`.
{% /step %}
{% step title="أعد تشغيل Codex" %}
هذا مهم حتى يلتقط marketplace والتغييرات المحلية.
{% /step %}
{% step title="افتح `/plugins`" %}
ابحث عن `OpenAI Docs Workshop` داخل السوق الصحيح.
{% /step %}
{% step title="ثبّت الإضافة وابدأ thread جديدة" %}
ثم جرّب:
`@openai-docs-workshop قارن بين صفحتين من وثائق OpenAI وأخرج checklist تنفيذية`
{% /step %}
{% /steps %}

{% accordion title="أخطاء شائعة في الورشة" open=true %}
- اسم plugin في `plugin.json` لا يطابق اسم entry في marketplace
- `source.path` غير صحيح أو غير نسبي
- تم تعديل plugin محليًا دون إعادة تشغيل Codex
- تم وضع `.mcp.json` أو `skills/` داخل `.codex-plugin/` بدل جذر الحزمة
{% /accordion %}

{% quickcheck
  prompt="في هذا المثال، ما الدور الأساسي لـ marketplace؟"
  options="استبدال `SKILL.md`|تعريف Codex بمكان Plugin وسياسات تثبيته|توليد OpenAI token"
  answer="2"
  explanation="marketplace هو الكتالوج الذي يسمح لـ Codex باكتشاف الإضافة وتثبيتها وإدارتها."
/%}

{% checkpoint title="بعد الورشة" %}
- لديك الآن blueprint عملي لإضافة Codex حقيقية
- skill وحدها لا تكفي للتوزيع
- marketplace هو جسر الاكتشاف والتثبيت
- MCP اختياري لكنه قوي عندما تحتاج tooling context حقيقي
{% /checkpoint %}
