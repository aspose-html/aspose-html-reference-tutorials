---
category: general
date: 2026-11-27
description: إنشاء مستند SVG وحفظ ملف SVG باستخدام بايثون. تعلم تصدير المتجه كـ SVG
  وإنشاء صورة SVG بسرعة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: ar
lastmod: 2026-11-27
og_description: إنشاء مستند SVG وحفظ ملف SVG باستخدام بايثون. يوضح لك هذا الدليل كيفية
  تصدير المتجه كملف SVG وإنتاج صورة SVG في دقائق.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: إنشاء مستند SVG وحفظ ملف SVG باستخدام بايثون
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: إنشاء مستند SVG وحفظ ملف SVG باستخدام بايثون
url: /ar/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند SVG وحفظ ملف SVG باستخدام Python

إذا كنت بحاجة إلى **create SVG document** من الصفر، فإن هذا الدليل يشرح لك العملية بالكامل. ستتعرف على كيفية **save SVG file** على القرص، وتصدير المتجه كـ SVG، والحصول على صورة SVG جاهزة للاستخدام في بضع أسطر من الشيفرة.

إنشاء رسومات قابلة للتوسع برمجياً مفيد للتقارير، أيقونات واجهة المستخدم، أو أي حالة تحتاج فيها إلى صور غير معتمدة على الدقة. بنهاية هذا الدليل ستكون قادرًا على الإجابة على سؤال “**how to create SVG**?” للأشكال البسيطة وتوسيع النمط إلى أعمال فنية متجهة معقدة.

## ما ستحتاجه

- Python 3.8 أو أحدث  
- حزمة `svgwrite` (قابلة للتثبيت عبر `pip`)  
- دليل قابل للكتابة لملف الإخراج  

لا يلزم أي محررات رسومات خارجية؛ كل شيء يعمل من سطر الأوامر.

## الخطوة 1: تثبيت مكتبة `svgwrite`

`svgwrite` توفر واجهة برمجة تطبيقات نظيفة وبايثونية لبناء ترميز SVG. قم بتثبيتها مرة واحدة باستخدام:

```bash
pip install svgwrite
```

> **نصيحة احترافية:** استخدم بيئة افتراضية (`python -m venv .venv`) للحفاظ على عزل الاعتمادات.

## الخطوة 2: إنشاء مستند SVG

الآن نقوم فعليًا **create SVG document** كائنات. تمثل الفئة `Drawing` العنصر الجذر `<svg>` وتتعامل مع المساحات الاسمية تلقائيًا.

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

مثيل `Drawing` هو نقطة الدخول لجميع عمليات SVG اللاحقة. من خلال تحديد `size` نحدد أبعاد اللوحة، مما يؤثر على طريقة عرض المتصفحات للصورة.

## الخطوة 3: إضافة عنصر دائرة حمراء

إضافة الأشكال أمر بسيط. طريقة `circle` تنشئ عنصر `<circle>`؛ ثم نرفعه إلى الجذر.

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

سبب اختيارنا للدائرة: الدوائر هي بدائيات متجهة تُظهر القابلية للتوسع دون أي فقدان للجودة، مما يجعل الناتج مثاليًا لاختبار سير عمل **export vector as SVG**.

## الخطوة 4: حفظ ملف SVG

أخيرًا، اكتب الترميز إلى القرص. هذه الخطوة تحقق متطلب **save SVG file** وتنتج ملفًا يمكنك فتحه في أي متصفح أو محرر متجهات.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

عند تشغيل السكريبت، سترى رسالة في وحدة التحكم تؤكد موقع الملف المُولد.

### النتيجة المتوقعة

ملف `circle.svg` الناتج يحتوي على:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

فتح الملف في المتصفح يعرض دائرة حمراء واضحة، وبما أنها مبنية على المتجهات يمكنك التكبير إلى ما لا نهاية دون تشويش.

## الخطوة 5: التغييرات الشائعة وحالات الحافة

### تصدير متجهات أكثر تعقيدًا

إذا كنت بحاجة إلى **export vector as SVG** لتوضيحات متعددة الأشكال، ببساطة كرّر نمط `dwg.add()` مع بدائيات أخرى (`rect`, `line`, `path`, إلخ). على سبيل المثال:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### التعامل مع Unicode والنص

SVG يدعم عناصر النص مع دعم كامل لـ Unicode. استخدم `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` لتضمين تسميات متعددة اللغات.

### حفظ في موقع مختلف

عند **save SVG image** إلى مجلد يحدده المستخدم، تحقق من المسار لتجنب أخطاء الأذونات:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### تصغير حجم الناتج

في خطوط الإنتاج، قد ترغب في حجم ملف أصغر. مرّر `pretty=False` إلى `dwg.tostring()` واكتب النتيجة يدويًا:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## كيفية إنشاء SVG باستخدام مكتبات بديلة (اختياري)

بينما `svgwrite` خفيفة الوزن ونقية‑Python، توجد أنظمة إيكولوجية أخرى:

- **cairosvg** – يحول PNG أو PDF أو HTML إلى SVG.  
- **lxml** – يتيح لك بناء ترميز SVG يدويًا باستخدام واجهات XML.  

اختيار المكتبة يعتمد على تعقيد مشروعك والاعتمادات الحالية.

## الخلاصة

أنت الآن تعرف كيف **create SVG document**، وتضيف أشكالًا متجهة، وت **save SVG file** باستخدام Python. الحل الكامل يوضح الخطوات لـ **export vector as SVG**، وإنشاء **SVG image**، والإجابة على السؤال الشائع **how to create SVG** برمجيًا.

من هنا يمكنك:
- توسيع السكريبت باستخدام الحلقات لتوليد مخططات أو أيقونات تلقائيًا.  
- دمج مخرجات SVG في تطبيقات الويب أو قوالب البريد الإلكتروني.  
- استكشاف الرسوم المتحركة بإضافة عناصر `<animate>` باستخدام `svgwrite`.  

جرّب أشكالًا، ألوانًا، وتدرجات مختلفة لتستفيد بالكامل من قوة الرسومات المتجهة القابلة للتوسع في مشاريع Python الخاصة بك. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مستند SVG – إضافة دائرة وحفظه كـ SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [إنشاء مستند SVG في Python – دليل تحويل SVG إلى PNG](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [تحميل ملف SVG Python – دليل كامل للتصدير، التضمين والتحويل](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}