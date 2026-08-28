---
category: general
date: 2026-05-28
description: تعلم كيفية استخدام SaveOptions لتقليص صفحات HTML في بايثون. يشرح هذا
  الدليل خطوة بخطوة أيضًا كيفية تحميل مستند HTML وإزالة الموارد المتداخلة بكفاءة.
draft: false
keywords:
- how to use saveoptions
- how to load html document
- how to trim html page
language: ar
og_description: كيفية استخدام SaveOptions لتقليص صفحات HTML في بايثون. اتبع هذا الدليل
  لتحميل مستند HTML، وتحديد حدود الموارد، وحفظ ملف نظيف وخفيف الوزن.
og_title: كيفية استخدام SaveOptions في بايثون – تقليم صفحات HTML
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to use SaveOptions to trim HTML pages in Python. This step‑by‑step
    guide also explains how to load an HTML document and efficiently remove nested
    resources.
  headline: How to Use SaveOptions in Python – Trim HTML Pages
  type: TechArticle
tags:
- python
- html-processing
- saveoptions
- resource-handling
title: كيفية استخدام SaveOptions في بايثون – تقليم صفحات HTML
url: /ar/python/general/how-to-use-saveoptions-in-python-trim-html-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام SaveOptions في بايثون – تقليم صفحات HTML

هل تساءلت يومًا **كيف تستخدم SaveOptions** لتقليص ملف HTML ضخم دون كسر أي شيء؟ لست وحدك. عندما تقوم بجلب صفحة تحتوي على عشرات الموارد المتداخلة — مثل CSS أو JS أو حتى مقتطفات HTML أخرى — قد ينتج عن ذلك ملف ضخم لا يمكن التحكم فيه.  

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يُظهر **كيفية استخدام SaveOptions**، بالإضافة إلى كيفية **تحميل مستند HTML** وأفضل طريقة **لتقليم صفحة HTML** عن طريق تحديد عمق التداخل. في النهاية ستحصل على ملف نظيف ومقلم جاهز للنشر أو المعالجة الإضافية.

## ما ستحققه

- تحميل أي ملف HTML محلي بسطر واحد من الكود.  
- تكوين خيارات معالجة الموارد لإيقاف العملية عند عمق تضمين معين.  
- حفظ النتيجة المقلمة باستخدام الفئة القوية `SaveOptions`.  

بدون أدوات خارجية، بدون سحر — فقط بايثون عادي ومكتبة صغيرة تقوم بالعمل الشاق.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك:

1. **Python 3.9+** مثبت (الصياغة المستخدمة تعمل على أي نسخة حديثة).  
2. حزمة `htmlprocessor` الافتراضية التي توفر `HTMLDocument` و `SaveOptions` و `ResourceHandlingOptions`. قم بتثبيتها عبر:

```bash
pip install htmlprocessor
```

> **نصيحة محترف:** إذا كنت تستخدم بيئة افتراضية، فعّلها أولًا — سيحافظ ذلك على نظافة التبعيات.

---

## الخطوة 1: كيفية تحميل مستند HTML

تحميل ملف بسيط مثل توجيه المُنشئ إلى مسار الملف. تقوم المكتبة بقراءة العلامات، وبناء شجرة شبيهة بـ DOM، وتجهّزها للمزيد من التلاعب.

```python
from htmlprocessor import HTMLDocument

# Replace with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/complex_page.html")
print("Document loaded –", doc.title or "Untitled")
```

> **لماذا هذا مهم:** كائن `HTMLDocument` يخفّف عنك التعامل مع السلاسل النصية الخام، ويمنحك طرقًا للاستعلام، والتعديل، وفي النهاية حفظ الصفحة. كما أنه يُوحّد نهايات الأسطر وترميزات الأحرف، مما يحفظك من الأخطاء الدقيقة لاحقًا.

ستلاحظ أننا طبعنا العنوان فقط للتحقق من نجاح التحميل. إذا كان الملف مفقودًا أو غير صالح، سيُطلق المُنشئ استثناءً واضحًا — بدون فشل صامت.

---

## الخطوة 2: تكوين معالجة الموارد – جوهر التقليم

الجزء التالي من اللغز هو **كيفية تقليم محتوى صفحة HTML** عن طريق تحديد مدى عمق متابعة المعالج للتضمينات. هنا تتألق `ResourceHandlingOptions`.

```python
from htmlprocessor import ResourceHandlingOptions

# Create a fresh options instance
res_opt = ResourceHandlingOptions()
# max_handling_depth = 2 means: main page + one level of includes
res_opt.max_handling_depth = 2
```

### ماذا يفعل `max_handling_depth`؟

- **العمق 1** → فقط ملف HTML الجذر، تُهمل جميع الموارد الخارجية.  
- **العمق 2** → الجذر بالإضافة إلى أي ملفات مُشار إليها مباشرة (مثل `iframe` أو تضمين من جانب الخادم).  
- **قيم أعلى** → تداخل أعمق، لكن أيضًا حجم إخراج أكبر ووقت معالجة أطول.

عن طريق تحديد العمق إلى **2**، نحتفظ بالصفحة الرئيسية وطبقة واحدة من التضمينات، متجاهلين أي شيء أعمق. هذا عادةً يكفي لإزالة التذييلات الزائدة، أو سكريبتات التحليل، أو القوالب المتداخلة التي لا تحتاجها في النسخة المقلمة.

---

## الخطوة 3: ربط الخيارات بتكوين الحفظ

الآن نربط قواعد الموارد الخاصة بنا بحدث `SaveOptions`. هذا الكائن يُخبر المكتبة *بالضبط* كيف تكتب الملف مرة أخرى إلى القرص.

```python
from htmlprocessor import SaveOptions

save_opt = SaveOptions()
save_opt.resource_handling_options = res_opt
```

> **لماذا نستخدم `SaveOptions`؟**  
> يمنحك تحكمًا دقيقًا في الإخراج — بخلاف عمق الموارد فقط. يمكنك لاحقًا إضافة ضغط، أو تنسيق جميل، أو حتى استدعاءات مخصصة دون تعديل منطق الحفظ الأساسي.

---

## الخطوة 4: كيفية استخدام SaveOptions لتقليم صفحة HTML

أخيرًا، نستدعي طريقة `save` مع الخيارات التي أعددناها. ستقوم المكتبة بتجوال شجرة DOM، واحترام حد العمق، وكتابة ملف مقلم.

```python
# Save the trimmed document
output_path = "YOUR_DIRECTORY/trimmed_page.html"
doc.save(output_path, save_opt)

print(f"Trimmed page saved to {output_path}")
```

### النتيجة المتوقعة

- ملف `trimmed_page.html` يحتوي على العلامات الأصلية **بالإضافة إلى** أي تضمينات حتى مستوى واحد عميق.  
- تُستبعد جميع التضمينات الأعمق، مما ينتج صفحة أصغر وأسرع تحميلًا.  
- لا تظهر وسوم مكسورة — المكتبة تغلق تلقائيًا أي عناصر تُركت معلقة بعد الإزالة.

يمكنك فتح النتيجة في المتصفح للتحقق من أن المحتوى الرئيسي لا يزال يُعرض، بينما تُزال السكريبتات أو الإطارات المتداخلة غير الضرورية.

---

## مثال كامل يعمل

بدمج كل ما سبق، إليك البرنامج الكامل الذي يمكنك نسخه ولصقه وتشغيله:

```python
# -*- coding: utf-8 -*-
"""
Trim an HTML page using SaveOptions.
Demonstrates:
- How to load an HTML document
- How to configure ResourceHandlingOptions
- How to use SaveOptions to save a trimmed version
"""

from htmlprocessor import HTMLDocument, SaveOptions, ResourceHandlingOptions

def trim_html(input_path: str, output_path: str, max_depth: int = 2) -> None:
    # Load the source document
    doc = HTMLDocument(input_path)
    print("Loaded:", doc.title or "Untitled")

    # Set up resource handling (how to trim HTML page)
    res_opt = ResourceHandlingOptions()
    res_opt.max_handling_depth = max_depth

    # Attach options to save configuration (how to use SaveOptions)
    save_opt = SaveOptions()
    save_opt.resource_handling_options = res_opt

    # Perform the save
    doc.save(output_path, save_opt)
    print(f"Trimmed HTML saved to {output_path}")

if __name__ == "__main__":
    INPUT = "YOUR_DIRECTORY/complex_page.html"
    OUTPUT = "YOUR_DIRECTORY/trimmed_page.html"
    trim_html(INPUT, OUTPUT, max_depth=2)
```

شغّل السكريبت، ووجّه المتغيّر `INPUT` إلى أي ملف HTML معقّد، وستحصل على نسخة أخف في `OUTPUT`.  

> **ملاحظة حول الحالات الخاصة:** إذا احتوت الصفحة الأصلية على تعليقات شرطية (`<!--[if IE]>…<![endif]-->`) تُشير إلى موارد أعمق، فسيتم حذفها كما هو الحال مع أي تضمين متداخل آخر. هذا يمنع حيل IE القديمة من تضخيم الحجم النهائي.

---

## ملخص بصري

فيما يلي مخطط سريع يوضح التدفق — من تحميل المستند، مرورًا بمعالجة الموارد، إلى حفظ النتيجة المقلمة.

![مثال على كيفية استخدام SaveOptions](https://example.com/placeholder.png "مخطط يوضح كيفية استخدام SaveOptions لتقليص صفحات HTML")

*النص البديل:* **مثال على كيفية استخدام SaveOptions** — يُظهر عملية من ثلاث خطوات: تحميل، تكوين، وحفظ مستند HTML.

---

## أسئلة شائعة ومشكلات محتملة

| السؤال | الجواب |
|----------|--------|
| **ماذا لو احتجت إلى تعمق أكبر؟** | زد `max_handling_depth` إلى 3 أو 4، لكن تذكر أن حجم الإخراج سيزداد. |
| **هل يمكنني استبعاد وسوم معينة (مثل `<script>`) بغض النظر عن العمق؟** | نعم — `SaveOptions` يدعم أيضًا خاصية `tag_exclusion_list`. أضف `"script"` إلى تلك القائمة لإزالة السكريبتات دائمًا. |
| **هل المكتبة آمنة للاستخدام في بيئات متعددة الخيوط؟** | النسخة الحالية ليست كذلك. أنشئ `HTMLDocument` منفصل لكل خيط. |
| **هل ستُعاد كتابة عناوين URL النسبية؟** | بشكل افتراضي لا. استخدم `save_opt.rewrite_relative_urls = True` إذا احتجت لتعديلها إلى الموقع الجديد. |

---

## الخطوات التالية

بعد أن أتقنت **كيفية استخدام SaveOptions**، جرّب هذه الإضافات:

- **ضغط الإخراج:** عيّن `save_opt.enable_gzip = True` للحصول على ملفات أصغر أثناء النقل.  
- **تنسيق جميل للتصحيح:** فعّل `save_opt.indent_output = True` للحصول على HTML منسق بشكل جميل.  
- **معالجة دفعات:** كرّر عبر مجلد من ملفات HTML وطبق نفس منطق التقليم — مفيد لمولدات المواقع الثابتة.

كل هذه التعديلات تُبنى على الأساس الذي تعلمته الآن، مما يحافظ على شفرتك نظيفة وقابلة للصيانة.

---

## الخاتمة

غطّينا دورة حياة كاملة لتقليص صفحة HTML في بايثون: **كيفية تحميل مستند HTML**، تكوين **كيفية تقليم صفحة HTML** باستخدام `ResourceHandlingOptions`، وأخيرًا **كيفية استخدام SaveOptions** لكتابة الملف المنقّح. المثال مستقل تمامًا، يعمل فورًا، ويظهر لماذا يُعد التحكم في عمق الموارد تحسينًا أساسيًا لتقنيات استخراج الويب، أو توليد المواقع الثابتة، أو أي سيناريو يتطلب لقطة HTML خفيفة الوزن.

جرّبه، واختبر قيمًا مختلفة لـ `max_handling_depth`، ودع الصفحات المقلمة تقوم بالعمل الشاق نيابةً عنك. إذا واجهت أي صعوبات، اترك تعليقًا أدناه — برمجة سعيدة!

## دروس ذات صلة

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Render HTML as PNG – Complete C# Guide](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)
- [How to Zip HTML in C# – Save HTML to Zip](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}