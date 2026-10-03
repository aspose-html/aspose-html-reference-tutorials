---
category: general
date: 2026-10-02
description: تعلم كيفية إنشاء مستند SVG في بايثون، حفظ SVG إلى ملف، وتصدير صورة SVG
  باستخدام سكريبت قصير وكامل.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: ar
lastmod: 2026-10-02
og_description: أنشئ مستند SVG في بايثون وصدر صورة SVG باستخدام هذا الدرس العملي.
  اتبع السكريبت، احفظ SVG إلى ملف، وأعد استخدام الرسوم المتجهة فورًا.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: إنشاء مستند SVG في بايثون – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: كيفية إنشاء مستند SVG وتصديره كصورة في بايثون
url: /ar/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تنشئ مستند SVG وتصديره كصورة في Python

إذا كنت بحاجة إلى **create SVG document** برمجيًا، يوضح لك هذا الدرس بالضبط كيفية القيام بذلك باستخدام Python. سترى سكريبتًا كاملًا يبني دائرة بسيطة، يحفظ الـ SVG إلى ملف، وينتج صورة SVG قابلة للتصدير يمكنك تضمينها في أي مكان.

إنشاء رسومات متجهة قابلة للتوسع من الكود يزيل الجهد اليدوي لرسم الأشكال في محرر واجهة المستخدم الرسومية. بنهاية هذا الدليل يمكنك دمج إنشاء SVG في خطوط أنابيب تصور البيانات، مولدات التقارير الآلية، أو أي مشروع يتطلب رسومات واضحة ومستقلة عن الدقة.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

- Python 3.8 أو أحدث مثبت
- مكتبة `svgwrite` (تثبيت عبر `pip install svgwrite`)
- صلاحية كتابة في الدليل الذي سيُحفظ فيه ملف SVG

هذه المتطلبات تجعل المثال خفيفًا ومتوافقًا مع أغلب البيئات.

## الخطوة 1: تثبيت واستيراد مكتبة SVG

الخطوة الأولى هي إضافة المكتبة الخارجية التي توفر واجهة برمجة تطبيقات مريحة لإنشاء SVG.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` تُجرد بنية XML لملف SVG، مما يتيح لك التركيز على الهندسة بدلاً من العلامات الخام.

## الخطوة 2: إنشاء كائن مستند SVG

الآن يمكنك **create SVG document** عن طريق إنشاء كائن `svgwrite.Drawing`. يمثل هذا الكائن العنصر الجذري `<svg>` ويحمل جميع الأشكال اللاحقة.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

معامل `size` يحدد أبعاد البكسل المعروضة، بينما `viewBox` يُنشئ نظام إحداثيات يتطابق مع الهندسة التي ستُعرّفها لاحقًا.

## الخطوة 3: إضافة عنصر دائرة

يتم تعريف الدائرة بمركزها (`cx`, `cy`) ونصف قطرها (`r`). استخدم الدالة المساعدة `circle` لإرفاق هذه الخصائص.

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

تقع الدائرة في وسط لوحة 100 × 100، مع ترك هامش 10 بكسل على كل جانب. عدّل `fill` و `stroke` لتتناسب مع لغة التصميم الخاصة بك.

## الخطوة 4: حفظ SVG إلى ملف

بعد تجميع الرسم، يمكنك **save SVG to file** باستخدام طريقة `save`. هذا يكتب XML منسقًا تفهمه المتصفحات ومحررات المتجهات.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

الملف `circle.svg` الآن موجود في دليل العمل الحالي. يمكنك فتحه في متصفح ويب، Inkscape، أو أي أداة تدعم صيغة SVG.

## الخطوة 5: التحقق من صورة SVG المُصدَّرة

افتح الملف المحفوظ في المتصفح لتأكيد النتيجة. يجب أن ترى دائرة متمركزة بالألوان المحددة. يبدو XML الخام كالتالي:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

نظرًا لأن SVG يعتمد على المتجهات، يمكنك تكبير الصورة دون فقدان الجودة، مما يجعله مثاليًا لتصاميم الويب المتجاوبة أو الطباعة عالية الدقة.

## نصيحة احترافية: تصدير SVG كـ PNG أو JPEG

إذا كنت بحاجة إلى نسخة نقطية، اجمع ملف SVG مع أداة تحويل مثل **CairoSVG**:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

تُظهر هذه الخطوة **export SVG image** إلى صيغة bitmap، وهو مفيد عندما لا تستطيع الأنظمة اللاحقة عرض SVG مباشرة.

## تنويعات شائعة وحالات حافة

| التنوع | كيفية التعامل |
|-----------|---------------|
| أشكال متعددة | استدعِ `dwg.add()` لكل عنصر جديد (rect, line, path). |
| أبعاد ديناميكية | احسب `size` و `viewBox` من البيانات قبل إنشاء `Drawing`. |
| تسميات نصية | استخدم `dwg.text("Label", insert=("10", "20"))` ونسّقها بـ `font_size` و `fill`. |
| إعادة استخدام المستند | احتفظ بكائن `Drawing` في الذاكرة واستدعِ `save()` كلما احتجت ملفًا محدثًا. |
| ملفات كبيرة | بثّ الإخراج باستخدام `dwg.tostring()` واكتب إلى كائن ملف يدويًا لتجنب الارتفاع المفاجئ في الذاكرة. |

معالجة هذه السيناريوهات تضمن أن سكريبت **how to generate SVG** الخاص بك يتوسع من أيقونات بسيطة إلى مخططات معقدة.

## ملخص السكريبت الكامل

فيما يلي المثال الكامل القابل للتنفيذ الذي يدمج جميع الخطوات والتحويل الاختياري:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

تشغيل هذا السكريبت ينتج `circle.svg`، وإذا تم تثبيت `cairosvg`، ينتج أيضًا `circle.png`. كلا الملفين جاهزان للإدراج في صفحات الويب، التقارير، أو المعالجة الإضافية.

## الخاتمة

أنت الآن تعرف كيف **create SVG document** في Python، **save SVG to file**، و**export SVG image** للاستخدام الأوسع. يغطي المثال استدعاءات API الأساسية، يوضح سبب أهمية كل خطوة، ويقدم امتدادات للرسومات الأكثر تعقيدًا.

بعد ذلك، استكشف مواضيع **SVG Python tutorial** إضافية مثل رسم المسارات، تطبيق التدرجات، وتحريك العناصر. سيمكنك دمج هذه التقنيات من توليد رسومات متجهة ديناميكية ومُستندة إلى البيانات مباشرة من تطبيقات Python الخاصة بك. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء وإدارة مستندات SVG في Aspose.HTML للـ Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [حفظ مستند SVG في Aspose.HTML للـ Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – تحويل SVG إلى صورة باستخدام Aspose.HTML للـ Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}