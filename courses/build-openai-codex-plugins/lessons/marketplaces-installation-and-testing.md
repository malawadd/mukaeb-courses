---
title: "Marketplaces والتثبيت والاختبار المحلي"
summary: "إنشاء `marketplace.json`، إضافة الإضافة إلى Codex، ثم اختبار التثبيت والتفعيل بشكل صحيح."
order: 5
durationLabel: "36 دقيقة"
type: "lesson"
isFreePreview: false
---

# Marketplaces والتثبيت والاختبار المحلي

الإضافة لا تصبح مرئية داخل `Codex` لمجرد وجودها على القرص. يجب أن تظهر عبر **Marketplace** يصف:

- اسم السوق أو الكتالوج
- الإضافات الموجودة داخله
- مكان كل Plugin
- سياسة التثبيت والمصادقة

## نوعا الـ marketplace الأساسيان

بحسب وثائق `Build plugins` هناك نمطان شائعان:

1. **Repo marketplace**
2. **Personal marketplace**

## Repo marketplace

يعيش في:

```text
$REPO_ROOT/.agents/plugins/marketplace.json
```

## مثال minimal لـ marketplace

```json
{
  "name": "local-repo",
  "plugins": [
    {
      "name": "my-plugin",
      "source": {
        "source": "local",
        "path": "./plugins/my-plugin"
      },
      "policy": {
        "installation": "AVAILABLE",
        "authentication": "ON_INSTALL"
      },
      "category": "Productivity"
    }
  ]
}
```

## طريقة الإضافة من CLI

الوثائق الحالية تدعم:

```bash
codex plugin marketplace add owner/repo
codex plugin marketplace add owner/repo --ref main
codex plugin marketplace add https://github.com/example/plugins.git --sparse .agents/plugins
codex plugin marketplace add ./local-marketplace-root
```

## بعد إنشاء marketplace ماذا أفعل؟

{% steps %}
{% step title="أعد تشغيل Codex" hint="مهم" %}
الوثائق تذكر إعادة تشغيل Codex بعد تحديث marketplace أو تعديل plugin المحلي.
{% /step %}
{% step title="افتح دليل الإضافات" %}
في CLI ادخل إلى `codex` ثم استخدم `/plugins`.
{% /step %}
{% step title="اختر marketplace الصحيح" %}
إذا كان لديك أكثر من مصدر، بدّل بين التبويبات واختر السوق الذي يضم إضافتك.
{% /step %}
{% step title="ثبّت الإضافة واختبرها" %}
ثبّت Plugin ثم افتح thread جديدة واطلب من Codex استخدامه، أو اذكره صراحة عبر `@`.
{% /step %}
{% /steps %}

{% accordion title="معلومة تشغيلية مهمة" %}
عندما يثبت Codex Plugin من marketplace، فإنه ينسخه إلى cache داخلي تحت `~/.codex/plugins/cache/...`، وللإضافات المحلية تكون النسخة `local`. لهذا قد تحتاج إعادة تشغيل Codex أو تحديث المصدر الذي يشير إليه marketplace بعد أي تعديل.
{% /accordion %}

{% quickcheck
  prompt="أين تضع repo marketplace عادة؟"
  options="`$REPO_ROOT/.agents/plugins/marketplace.json`|داخل `.codex-plugin/`|داخل `skills/`"
  answer="1"
  explanation="هذا هو الموقع الموثق للـ repo-scoped marketplace في Codex."
/%}

{% checkpoint title="قواعد التثبيت السليم" %}
- أنشئ marketplace أولًا
- اضبط `source.path` بدقة
- أعد تشغيل Codex بعد التعديلات
- اختبر التثبيت ثم اختبر الاستدعاء داخل thread جديدة
{% /checkpoint %}
