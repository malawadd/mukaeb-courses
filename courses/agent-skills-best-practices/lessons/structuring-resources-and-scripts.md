---
title: "تنظيم references وscripts وassets"
summary: "فصل المعرفة والتنفيذ والأصول داخل Skill بدل حشرها كلها في SKILL.md."
order: 5
durationLabel: "23 دقيقة"
type: "lesson"
isFreePreview: false
---

# تنظيم references وscripts وassets

أحد أكبر التحولات بين Skill مبتدئة وSkill احترافية هو معرفة **ما الذي يبقى داخل `SKILL.md`، وما الذي يجب إخراجه إلى ملفات مساعدة**.

{% callout title="التقسيم هنا ليس تجميلًا" tone="tip" %}
كل ملف إضافي يجب أن يخدم غرضًا واضحًا: تقليل الغموض، تقليل استهلاك السياق، أو زيادة الحتمية في التنفيذ.
{% /callout %}

## متى تستخدم `references/`؟

استخدم `references/` عندما تكون لديك معرفة لا تحتاج إلى تحميلها دائمًا، مثل:

- جداول أو schemas أو checklists طويلة
- توثيق خاص بإطار أو مزود محدد
- preservation rules أو formatting guides
- ملفات variant-specific مثل `aws.md` و`gcp.md`

## متى تستخدم `scripts/`؟

استخدم `scripts/` عندما يكون لديك عمل متكرر أو حساس للدقة، مثل:

- تشغيل متصفح واختبار واجهة
- تحويل ملفات أو ضغط محتوى أو استخراج بيانات
- توليد تقارير أو artifacts
- جلب بيانات live من مصدر معروف

بدل أن تقول للوكيل "اكتب سكربت صغيرًا كل مرة"، أعطه سكربتًا جاهزًا يمكنه استدعاؤه مباشرة.

## متى تستخدم `assets/`؟

استخدم `assets/` للملفات التي تساعد في الإخراج النهائي:

- قوالب HTML أو PowerPoint أو Markdown
- خطوط أو صور أو أيقونات
- ملفات showcase أو أمثلة بصرية

## نمط progressive disclosure

{% steps %}
{% step title="ابدأ بقرار صغير" hint="في SKILL.md" %}
اشرح كيف يقرر الوكيل هل يحتاج المرجع أو السكربت أصلًا.
{% /step %}
{% step title="أحِل إلى الملف المناسب" %}
قل صراحة: افتح `references/foo.md` عند العمل على الحالة الفلانية، أو شغّل `scripts/bar.py --help` قبل قراءة المصدر.
{% /step %}
{% step title="لا تحمّل الوكيل كل شيء" %}
إذا كان لديك 10 مراجع، لا تطلب منه قراءتها كلها. وجّهه إلى أصغر جزء ذي صلة.
{% /step %}
{% step title="اجعل الاستدعاء قابلًا للتنفيذ" %}
اكتب أسماء الملفات والمسارات والأوامر بوضوح حتى لا يضطر الوكيل للتخمين.
{% /step %}
{% /steps %}

## خطأ شائع

{% accordion title="الخطأ: نقل الفوضى من ملف واحد إلى عشرة ملفات" open=true %}
الفصل لا يفيد إذا لم يكن هناك منطق واضح. لا تنشئ `references/` و`scripts/` ثم تترك الوكيل يبحث فيها عشوائيًا. يجب أن يعرف: متى يفتح أي ملف، ولماذا، وما الذي يتوقع أن يجده هناك.
{% /accordion %}

## قالب بنية مقترح

```text
my-skill/
├── SKILL.md
├── references/
│   ├── checklist.md
│   └── provider-a.md
├── scripts/
│   └── run_task.py
└── assets/
    └── output-template.html
```

{% quickcheck
  prompt="ما أفضل مكان لجدول طويل يشرح naming patterns متعددة لا تحتاجها كل مرة؟"
  options="داخل أول 20 سطرًا من SKILL.md|references/|اسم المجلد فقط"
  answer="2"
  explanation="المرجع الطويل مكانه الطبيعي في `references/` حتى يبقى الملف الرئيسي خفيفًا وموجّهًا."
/%}

{% checkpoint title="الخلاصة العملية" %}
- `SKILL.md` يوجّه.
- `references/` تحفظ المعرفة.
- `scripts/` تنفّذ.
- `assets/` تثبّت شكل الإخراج.
{% /checkpoint %}
