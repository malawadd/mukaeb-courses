---
title: "تشريح الإضافة: manifest والبنية الصحيحة"
summary: "بناء `.codex-plugin/plugin.json` وفهم الحقول المطلوبة والاختيارية ومسارات الملفات."
order: 2
durationLabel: "30 دقيقة"
type: "lesson"
isFreePreview: false
---

# تشريح الإضافة: manifest والبنية الصحيحة

المدخل الإجباري لأي Plugin في `Codex` هو:

```bash
.codex-plugin/plugin.json
```

ووفقًا لوثائق `Build plugins` فهذا الملف هو **entry point** الذي يعرّف الإضافة، بينما بقية الملفات اختيارية لكن شائعة جدًا في الإضافات المنشورة داخليًا أو الموزعة على فرق.

## أبسط نسخة ممكنة

```json
{
  "name": "my-first-plugin",
  "version": "1.0.0",
  "description": "Reusable greeting workflow",
  "skills": "./skills/"
}
```

{% callout title="قاعدة التسمية" tone="note" %}
استخدم اسمًا ثابتًا بصيغة `kebab-case`. وثائق Codex تنص على أن `name` يُستخدم كمُعرّف للإضافة وكـ namespace داخلي.
{% /callout %}

## البنية التي يتوقعها Codex

```bash
my-plugin/
  .codex-plugin/
    plugin.json
  skills/
    my-skill/
      SKILL.md
  .mcp.json
  .app.json
  assets/
```

## لماذا هذه البنية مهمة؟

لأن Codex يفرّق بين:

- ملف manifest نفسه
- المكوّنات المضمّنة مثل skills وapps وMCP
- الأصول البصرية المستخدمة في واجهة التثبيت

ولا تريد خلط هذه الطبقات أو وضعها في أماكن يصعب على Codex اكتشافها.

## Manifest أغنى وأكثر واقعية

```json
{
  "name": "openai-docs-workshop",
  "version": "0.1.0",
  "description": "Bundle reusable OpenAI docs workflows for Codex.",
  "author": {
    "name": "Mukaeb Academy",
    "email": "academy@example.com",
    "url": "https://example.com"
  },
  "homepage": "https://example.com/plugins/openai-docs-workshop",
  "repository": "https://github.com/example/openai-docs-workshop",
  "license": "MIT",
  "keywords": ["openai", "codex", "docs", "plugins"],
  "skills": "./skills/",
  "mcpServers": "./.mcp.json",
  "apps": "./.app.json",
  "interface": {
    "displayName": "OpenAI Docs Workshop",
    "shortDescription": "Skills and docs tooling for OpenAI builders",
    "longDescription": "Distribute reusable OpenAI docs workflows with optional MCP and app integrations.",
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
    "brandColor": "#10A37F",
    "composerIcon": "./assets/icon.png",
    "logo": "./assets/logo.png",
    "screenshots": ["./assets/screenshot-1.png"]
  }
}
```

## الوظائف الثلاثة للـ manifest

في الوثائق الرسمية، manifest الجيد يقوم بثلاث وظائف:

1. يعرّف الإضافة.
2. يشير إلى المكوّنات المضمّنة مثل skills وapps وMCP.
3. يزوّد Codex ببيانات العرض والتقديم مثل الوصف والأيقونات والروابط القانونية.

## قواعد المسارات

- اجعل المسارات **relative** وتبدأ بـ `./`
- ضع `skills/` و`assets/` و`.mcp.json` و`.app.json` في جذر الإضافة
- لا تضع داخل `.codex-plugin/` إلا `plugin.json`

{% quickcheck
  prompt="أي مسار يجب أن يكون داخل `.codex-plugin/`؟"
  options="`skills/`|`assets/`|`plugin.json` فقط"
  answer="3"
  explanation="الوثائق تنص على أن `plugin.json` هو الملف الوحيد الذي يجب أن يعيش داخل `.codex-plugin/`."
/%}

{% checkpoint title="خلاصة البنية" %}
- نقطة الدخول الإلزامية: `.codex-plugin/plugin.json`
- بقية المكونات تكون عند جذر الإضافة
- استخدم `./` في كل المسارات النسبية
- اعتبر `interface` جزءًا أساسيًا من جودة تجربة التثبيت، لا حشوًا تجميليًا
{% /checkpoint %}
