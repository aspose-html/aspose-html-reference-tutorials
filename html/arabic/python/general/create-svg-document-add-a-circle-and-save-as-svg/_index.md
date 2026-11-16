---
category: general
date: 2026-07-31
description: تعلم كيفية إنشاء مستند SVG، إضافة دائرة، وحفظ ملف SVG بسرعة. صدّر الرسمة
  كـ SVG ببضع أسطر من كود بايثون.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: ar
lastmod: 2026-07-31
og_description: إنشاء مستند SVG، إضافة دائرة، وحفظ ملف SVG في ثوانٍ. يوضح لك هذا الدليل
  كيفية تصدير الرسم كملف SVG مع كود واضح وقابل للتنفيذ.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: إنشاء مستند SVG – إضافة دائرة وحفظه كملف SVG
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: إنشاء مستند SVG – إضافة دائرة وحفظه كـ SVG
url: /ar/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند SVG – إضافة دائرة وحفظه كملف SVG

هل احتجت يوماً إلى **إنشاء مستند SVG** من الشيفرة ولكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك؛ يواجه العديد من المطورين هذا العائق عندما يبدؤون أول مرة مع الرسومات المتجهة. في هذا الدرس سنستعرض مثالًا صغيرًا ومستقلاً يوضح لك كيفية **إضافة دائرة إلى SVG**، ثم **حفظ ملف SVG** بحيث يمكنك **تصدير الرسم كملف SVG** للاستخدام على الويب أو في أدوات التصميم.

سنحافظ على البساطة: بضع أسطر من بايثون، مكتبة مساعدة شائعة للـ SVG، وقليل من الشرح. في النهاية ستحصل على ملف `circle.svg` جاهز في مجلدك، وستفهم لماذا كل خطوة مهمة—بدون اختصارات “انظر الوثائق”.

## ما ستحتاجه

- Python 3.8+ (أي نسخة حديثة تعمل)
- حزمة `svgwrite` – ثبّتها باستخدام `pip install svgwrite`
- محرر نصوص أو بيئة تطوير (VS Code، PyCharm، أو حتى Notepad يكفي)
- صلاحية كتابة في الدليل الذي تريد حفظ الملف فيه

هذا كل شيء. لا تبعيات ثقيلة، ولا خدمات خارجية.

## الخطوة 1: إعداد مستند SVG

إنشاء مستند SVG سهل كإنشاء كائن `Drawing` من مكتبة `svgwrite`. فكر في هذا الكائن كقماش فارغ حيث تعيش كل الأشكال.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **لماذا هذا مهم:** فئة `Drawing` تتولى كل تفاصيل XML الأساسية لك—المساحات الاسمية، الرؤوس، وعنصر الجذر `<svg>`. بتحديد اسم الملف مسبقًا نعرف بالفعل أين سيُحفظ الملف، مما يجعل خطوة **حفظ ملف SVG** لاحقًا بسيطة.

### نصيحة احترافية
إذا كنت تخطط لإنشاء ملفات متعددة داخل حلقة، أعط كل `Drawing` اسمًا فريدًا أو استخدم `io.BytesIO` للاحتفاظ بكل شيء في الذاكرة حتى تكون جاهزًا للكتابة.

## الخطوة 2: إضافة دائرة إلى SVG

الآن بعد أن المستند موجود، لنـ **نضيف دائرة إلى SVG**. طريقة `add()` تقبل أي كائن شكل؛ `Circle` مثالية لنقطة حمراء بسيطة في المركز.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **لماذا نستخدم المتغيرين `center` و `radius`:** كتابة القيم مباشرة تجعل الشيفرة أصعب قراءة وصيانة. بتسمية القيم نوضح النية—هذه الدائرة تقع في وسط لوحة 200 × 200 وتكون كبيرة بما يكفي لتُلاحظ.

### حالة خاصة – خلفية شفافة
إذا كنت تحتاج خلفية شفافة (وهي الافتراضية للـ SVG)، يمكنك تجاهل تعيين `fill` على الجذر. للحصول على خلفية بيضاء، أضف:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

ضع هذا قبل إضافة الدائرة بحيث يكون المستطيل تحتها.

## الخطوة 3: حفظ ملف SVG

مع وجود الشكل، الخطوة الأخيرة هي **حفظ ملف SVG**. طريقة `save()` تكتب XML إلى القرص، وبما أننا قد أعطينا `Drawing` اسم ملف، فإن استدعاء واحد يكفي.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **ماذا يحدث خلف الكواليس؟** تقوم `svgwrite` بتسلسل شجرة العناصر إلى سلسلة نصية، وتضيف إعلان XML، وتكتبها بترميز UTF‑8. إذا لم يكن الدليل الهدف موجودًا، سيُطلق بايثون استثناء `FileNotFoundError`؛ تأكد من صحة المسار أو أنشئه باستخدام `os.makedirs()`.

### إضافي: تصدير الرسم كـ SVG برمجيًا

إذا كنت تحتاج محتوى الـ SVG كسلسلة نصية—مثلاً لتضمينه في بريد إلكتروني HTML—يمكنك استدعاء `dwg.tostring()` بدلاً من `save()`:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## مثال كامل يعمل

نجمع كل ما سبق في سكريبت كامل جاهز للتنفيذ:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**الناتج المتوقع:** بعد تشغيل السكريبت، ستظهر لك ملف `circle.svg` في نفس المجلد. فتحه في المتصفح أو أي محرر متجه سيظهر دائرة حمراء متمركزة على مربع أبيض—تمامًا ما برمجناه.

## أسئلة شائعة ومشكلات محتملة

- **ماذا لو أردت شكلاً مختلفًا؟** استبدل `dwg.circle` بـ `dwg.rect` أو `dwg.ellipse` أو حتى سلسلة `<path>` مخصصة. الـ API ثابت عبر الأشكال.
- **هل يمكن تضمين الـ SVG مباشرة في HTML؟** بالطبع. الملف الذي أنشأته يمكن الإشارة إليه بـ `<img src="circle.svg" alt="Red circle">` أو تضمينه داخل وسوم `<svg>`.
- **لماذا لا نكتب XML يدويًا؟** يمكنك ذلك، لكن مكتبات مثل `svgwrite` تتعامل مع تعقيدات المساحات الاسمية وتجعل الشيفرة أكثر قابلية للصيانة—خاصةً عندما تبدأ بإضافة تدرجات أو تحريكات.

## الخلاصة

الآن تعرف كيف **تنشئ مستند SVG**، **تضيف دائرة إلى SVG**، و**تحفظ ملف SVG** لتتمكن من **تصدير الرسم كملف SVG** ببضع أسطر من بايثون فقط. النمط قابل للتوسيع: استبدل الدائرة بأي شكل متجه، أو أنشئ مخططات عبر حلقة بيانات، أو عالج مجموعة من الأصول لنظام تصميم.

ما الخطوة التالية؟ جرّب إضافة تسميات نصية، أو تجربة التدرجات، أو توليد معرض كامل من الأيقونات في سكريبت واحد. إذا كنت ترغب في استكشاف ميزات متقدمة، اطلع على توثيق `svgwrite` حول المجموعات (`<g>`)، التحويلات، ودعم التحريكات.

برمجة سعيدة، ولتظل رسوماتك المتجهة دائمًا حادة!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}