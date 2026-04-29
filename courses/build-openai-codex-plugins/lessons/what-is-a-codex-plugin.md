---
title: "ما هي إضافة Codex أصلًا؟"
summary: "فهم دور الـ Plugin داخل Codex والفرق بينه وبين Skills المحلية وApps SDK وMCP."
order: 1
durationLabel: "18 دقيقة"
type: "lesson"
isFreePreview: true
---

# ما هي إضافة Codex أصلًا؟

في وثائق `Codex` الحالية، الإضافة أو **Plugin** ليست مجرد ملف إعداد صغير، بل **وحدة توزيع قابلة للتثبيت** يمكنها أن تجمع:

- skill واحدة أو أكثر
- إعدادات `MCP`
- ربطًا مع `Apps`
- وأصولًا مرئية مثل الشعار واللقطات والوصف

{% callout title="الفكرة الأساسية" tone="tip" %}
فكّر في `Skill` على أنها workflow مكتوب، بينما `Plugin` هو الغلاف القابل للتثبيت الذي يوزع هذا workflow على أشخاص آخرين داخل Codex.
{% /callout %}

{% video
  title="مقدمة رسمية إلى Codex"
  src="https://academy.openai.com/home/videos/introduction-to-codex-2026-03-02"
  caption="فيديو تمهيدي من OpenAI Academy يساعدك على وضع الإضافات داخل الصورة الأكبر لسير العمل في Codex."
/%}

## لماذا أحتاج Plugin بدل Skill فقط؟

وفقًا لوثائق `Codex`، يظل `Skill` ممتازًا عندما تعمل محليًا داخل repo واحد أو تريد تجربة workflow بسرعة. لكن عندما تريد:

- مشاركة workflow مع فريق كامل
- تجميع أكثر من skill في حزمة واحدة
- إرفاق `MCP server` أو `app mappings`
- جعل الإضافة تظهر في Plugin Directory

فهنا يصبح الـ `Plugin` هو الخيار الصحيح.

## الفرق بين المفاهيم الأساسية

{% tabs %}
{% tab label="Skill" %}
هي صيغة التأليف نفسها. تكتب `SKILL.md` مع تعليمات ووصف وربما `scripts/` و`references/`.
{% /tab %}
{% tab label="Plugin" %}
هو وحدة التوزيع القابلة للتثبيت في Codex. يمكنه أن يضم skills وMCP وApps وأصول العرض.
{% /tab %}
{% tab label="MCP" %}
هو طبقة ربط الأدوات والخوادم والموارد السياقية. قد تضع إعداداته داخل `.mcp.json` كجزء من الإضافة.
{% /tab %}
{% tab label="Apps SDK" %}
هذا مسار مختلف يخص بناء تطبيقات لـ ChatGPT. قد تشير الإضافة إلى `apps`، لكن Apps SDK ليس هو نفسه Plugin الخاص بـ Codex.
{% /tab %}
{% /tabs %}

## أين يستخدم Codex الإضافات؟

في وثائق OpenAI، الإضافات تعمل عبر أسطح Codex المختلفة:

- `Codex app`
- `Codex CLI`
- امتداد الـ IDE

وبعد تثبيت الإضافة يمكن للمستخدم:

- أن يطلب النتيجة مباشرة ويترك Codex يختار الأداة المناسبة
- أو يذكر الإضافة صراحة باستخدام `@`
- أو يذكر إحدى skills المضمنة داخل الإضافة

## متى لا تبدأ بـ Plugin؟

{% accordion title="ابدأ بـ Skill أولًا عندما..." open=true %}
- ما زلت تستكشف الفكرة
- الـ workflow يخص repo واحدًا فقط
- لا توجد حاجة فعلية لواجهة تثبيت أو marketplace
- لا تحتاج ربطًا مع Apps أو MCP بعد
{% /accordion %}

## كيف تصف قرارك المعماري؟

{% steps %}
{% step title="اكتب workflow محليًا" hint="بأقل تكلفة" %}
ابدأ بـ skill واحدة تتأكد بها أن المشكلة حقيقية ومتكررة.
{% /step %}
{% step title="تحقق من الحاجة للتوزيع" %}
إذا احتاج زملاؤك نفس workflow أو احتجت تغليفه مع إعدادات إضافية، انتقل إلى Plugin.
{% /step %}
{% step title="أضف طبقات الربط" %}
عند الحاجة، أضف `MCP` أو `Apps` أو metadata مرئية حتى تصبح الإضافة جاهزة للتثبيت والاكتشاف.
{% /step %}
{% /steps %}

{% quickcheck
  prompt="ما الوصف الأدق للـ Plugin في Codex؟"
  options="بديل لـ SKILL.md فقط|وحدة توزيع قابلة للتثبيت يمكن أن تضم skills وMCP وApps|نوع جديد من نماذج OpenAI"
  answer="2"
  explanation="الـ Plugin هو الحزمة القابلة للتثبيت، بينما skill هي صيغة workflow نفسها."
/%}

{% checkpoint title="قبل المتابعة" %}
- `Skill` تكتب السلوك.
- `Plugin` يوزع السلوك.
- `MCP` يربطك بالأدوات والموارد.
- `Apps SDK` يخص بناء تطبيقات ChatGPT، وليس مرادفًا لإضافة Codex.
{% /checkpoint %}
