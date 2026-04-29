---
title: "ربط Plugin مع MCP وApps"
summary: "فهم دور `.mcp.json` و`.app.json` ومتى تستخدم كل واحد منهما، مع توضيح الفرق عن Apps SDK."
order: 4
durationLabel: "34 دقيقة"
type: "lesson"
isFreePreview: false
---

# ربط Plugin مع MCP وApps

أحد أهم أسباب الانتقال من skill محلية إلى Plugin هو أنك تريد **تغليف أكثر من مجرد تعليمات**. هنا يدخل دور:

- `.mcp.json`
- `.app.json`

## ماذا يعني `mcpServers`؟

في manifest يمكن أن تضع:

```json
{
  "mcpServers": "./.mcp.json"
}
```

وهذا يعني أن الإضافة تشير إلى إعداد MCP servers مضمّن في نفس الحزمة. هذه البنية مفيدة عندما تحتاج skill إلى:

- الوصول إلى docs server
- تشغيل connector داخلي
- أو فتح قناة موحدة لقراءة موارد أو تنفيذ أدوات

## ماذا يعني `apps`؟

في manifest يمكن أيضًا أن تضع:

```json
{
  "apps": "./.app.json"
}
```

والمقصود هنا هو **ربط الإضافة مع App أو Connector mappings** التي يمكن أن تُستخدم عبر أسطح OpenAI المناسبة.

{% callout title="تمييز مهم" tone="warning" %}
وجود `apps` داخل Plugin لا يعني أن Plugin نفسه هو Apps SDK project. Plugin في Codex هو وحدة تثبيت وتوزيع، بينما Apps SDK هو مسار تطوير لتطبيقات ChatGPT.
{% /callout %}

## كيف نفسر العلاقة بين Plugin وApps SDK؟

وثائق `Apps SDK` الحالية تشرح أن ChatGPT يدعم معيار `MCP Apps`، وأن بناء UI محمول يبدأ من المعيار المفتوح ثم يمكن تعزيزُه بامتدادات خاصة بـ ChatGPT عند الحاجة.

{% tabs %}
{% tab label="Codex Plugin" %}
غرضه أن يوزع workflows قابلة للتثبيت داخل Codex، مع Skills وMCP وApps وmetadata.
{% /tab %}
{% tab label="Apps SDK" %}
غرضه أن يبني تطبيقات أو واجهات مدمجة داخل ChatGPT، غالبًا مع UI ومكونات وطرق توصيل مختلفة.
{% /tab %}
{% tab label="MCP Apps" %}
هو المعيار المفتوح الذي يجعل بعض واجهات التطبيقات أكثر قابلية للنقل بين hosts متوافقة.
{% /tab %}
{% /tabs %}

## متى أضيف `.mcp.json`؟

أضفه عندما تحتاج الإضافة إلى خادم MCP حقيقي أو إعدادات ready-made، مثل:

- docs lookup
- internal knowledge base
- API wrappers
- أدوات بحث أو ملفات

مثال تصوري:

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

## كيف تبني قرارًا معماريًا صحيحًا؟

{% steps %}
{% step title="ابدأ بالحد الأدنى" hint="لا تفرط في التجميع" %}
إذا كانت القيمة كلها في skill واحدة، فلا تضف `.mcp.json` أو `.app.json` إلا إذا كانت هناك حاجة تشغيلية فعلية.
{% /step %}
{% step title="اسأل: هل dependency جزء من الحزمة؟" %}
إذا كان المستخدم لا يستطيع تشغيل الـ workflow بدون أداة خارجية أو docs server، فغالبًا يجب تغليفها داخل الإضافة.
{% /step %}
{% step title="افصل بين التوزيع والواجهة" %}
Plugin يوزع. Apps SDK يبني تجربة تطبيق. لا تخلط بين مسؤولية الاثنين.
{% /step %}
{% /steps %}

{% quickcheck
  prompt="متى يكون من المنطقي إضافة `.mcp.json` إلى Plugin؟"
  options="عندما أريد تغيير لون البطاقة|عندما يحتاج workflow إلى MCP server أو tooling context حقيقي|عندما أريد استبدال `plugin.json`"
  answer="2"
  explanation="`.mcp.json` يخص ربط خوادم MCP أو إعداداتها، لا metadata البصرية."
/%}

{% checkpoint title="التمييز الذي يجب ألا يضيع" %}
- `mcpServers` يشير إلى `.mcp.json`
- `apps` يشير إلى `.app.json`
- Plugin قد يضم هذه الأشياء لكنه ليس هو نفسه Apps SDK project
- أضف كل طبقة فقط عندما تضيف قيمة تشغيلية حقيقية
{% /checkpoint %}
