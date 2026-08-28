---
category: general
date: 2026-05-31
description: تعلم كيفية الحصول على عنصر بواسطة المعرف، تغيير لون خلفية HTML، قراءة
  نص HTML وتعيين سمة HTML باستخدام بايثون. دليل خطوة بخطوة.
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: ar
og_description: احصل على العنصر بالمعرف، اقرأ نص HTML، عيّن سمة HTML وغير لون الخلفية
  باستخدام بايثون في دليل واحد سهل المتابعة.
og_title: الحصول على العنصر بواسطة المعرف في بايثون – دليل كامل لتعديل HTML
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  headline: Get element by id in Python – Complete HTML Manipulation Guide
  type: TechArticle
- description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  name: Get element by id in Python – Complete HTML Manipulation Guide
  steps:
  - name: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
    text: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
  - name: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
    text: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
  - name: '**Retrieves** the element using **get element by id**.'
    text: '**Retrieves** the element using **get element by id**.'
  - name: '**Prints** the element’s text—showing **how to read HTML text**.'
    text: '**Prints** the element’s text—showing **how to read HTML text**.'
  - name: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
    text: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
  - name: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
    text: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
  - name: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
    text: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
  type: HowTo
tags:
- python
- html
- web‑scraping
title: الحصول على العنصر حسب المعرف في بايثون – دليل شامل لتعديل HTML
url: /ar/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# الحصول على العنصر بواسطة المعرف (id) في بايثون – دليل شامل لتعديل HTML

هل احتجت يوماً إلى **get element by id** من صفحة HTML أثناء كتابة سكربت بايثون سريع؟ لست وحدك—معظم المطورين يواجهون هذه العقبة عندما يبدأون في زحف المواقع أو تعديل التقارير المحلية. الخبر السار؟ ببضع أسطر من الكود يمكنك قراءة نص العنصر، تغيير لون الخلفية، وحتى تعيين سمات جديدة، كل ذلك دون مغادرة محررك.

في هذا الدرس سنستعرض مثالاً عملياً: تحميل ملف `sample.html` المحلي، استخراج العنصر الذي معرفه `main‑content`، طباعة النص الداخلي له، وأخيراً استبدال لون الخلفية إلى رمادي فاتح. في النهاية ستعرف **how to read HTML text**، **how to set HTML attribute**، ولماذا **manipulate HTML with Python** مهارة مفيدة في أي صندوق أدوات أتمتة.

## ما ستحتاجه

- **Python 3.9+** (أي نسخة حديثة تعمل)
- مكتبة **`lxml`** (أو **BeautifulSoup** إذا تفضّل) – سنستخدم `lxml.html` لأنها توفر واجهة `get_element_by_id` مشابهة.
- ملف HTML صغير اسمه `sample.html` موجود في مجلد اسمه `YOUR_DIRECTORY`. يمكنك نسخ المقتطف أدناه إلى ذلك الملف:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Demo Page</title>
</head>
<body>
    <div id="main-content">
        Hello, world! This is the original text.
    </div>
</body>
</html>
```

هذا كل شيء—لا أطر عمل معقدة، مجرد بايثون عادي وملف HTML ثابت.

## الخطوة 1: تثبيت المكتبة المطلوبة

إذا لم تقم بتثبيت `lxml` بعد، افتح الطرفية وشغّل:

```bash
pip install lxml
```

*نصيحة احترافية:* استخدام بيئة افتراضية يحافظ على نظافة تثبيت بايثون العام، خاصةً عندما تبدأ في التعامل مع مشاريع متعددة.

## الخطوة 2: تحميل مستند HTML

الآن سنقرأ الملف إلى كائن مستند `lxml.html`. فكر في ذلك كتحويل النص الخام إلى شجرة قابلة للتنقل.

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

تشغيل هذا سيطبع “Document loaded successfully.” إذا تعذر العثور على الملف، سيُطلق بايثون استثناء `FileNotFoundError`—من الجيد التقاطه مبكراً قبل مطاردة عنصر وهمي.

## الخطوة 3: الحصول على العنصر بواسطة المعرف (id)

هذا هو جوهر الموضوع. `lxml` يوفّر لنا طريقة مريحة `get_element_by_id` التي تحاكي واجهة DOM التي تستخدمها في JavaScript.

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

عند وجود العنصر، سترى “Element found!” مطبوعاً في وحدة التحكم. هذه هي خطوة **get element by id** التي تشغّل معظم التعديلات اللاحقة.

## الخطوة 4: كيفية قراءة نص HTML

بمجرد حصولك على العنصر، استخراج النص الظاهر له سهل جداً. طريقة `text_content()` تُعيد كل ما داخل العنصر، مُزالةً العلامات.

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

الناتج المتوقع:

```
Inner text: Hello, world! This is the original text.
```

قد تتساءل، *ماذا لو كان العنصر يحتوي على وسوم متداخلة؟* `text_content()` ما زالت تعمل—إنها تُدمج جميع عقد النص التابعة، وتُعطيك سلسلة نظيفة يمكنك تسجيلها، تخزينها، أو تمريرها إلى خوارزمية أخرى.

## الخطوة 5: كيفية تعيين سمة HTML

تغيير أو إضافة سمات يكون بنفس السهولة. طريقة `set` تسمح لك بتعيين أي اسم سمة ترغب به.

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

الناتج:

```
New attribute value: true
```

هذا السطر يوضح **how to set HTML attribute** في الوقت الفعلي. يمكنك استبدال `"data-modified"` بـ `"class"`، `"title"` أو أي سمة أخرى يدعمها العنصر.

## الخطوة 6: تغيير لون الخلفية في HTML

الآن إلى التعديل البصري. لتغيير لون الخلفية، نُضيف سمة `style` التي تتجاوز الإعداد الافتراضي.

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

بعد تشغيل السكربت، سيظهر الـ `div` في `sample.html` هكذا عند فتحه في المتصفح:

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

هذه هي تقنية **change background colour html** التي يمكنك إعادة استخدامها لأي عنصر—فقط غيّر قيمة اللون.

## الخطوة 7: تعديل HTML باستخدام بايثون – تجميع كل شيء

فيما يلي السكربت الكامل القابل للتنفيذ الذي يجمع جميع الخطوات. احفظه باسم `modify_html.py` وشغّله من نفس الدليل الذي يحتوي على مجلد `YOUR_DIRECTORY`.

```python
#!/usr/bin/env python3
"""
Complete example: load an HTML file, get element by id,
read its text, set a new attribute, and change its background colour.
"""

from lxml import html
import pathlib
import sys

def main():
    # 1️⃣ Load the document
    html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")
    try:
        doc = html.parse(str(html_path)).getroot()
    except OSError as e:
        sys.exit(f"Failed to read HTML file: {e}")

    # 2️⃣ Get element by id
    elem = doc.get_element_by_id("main-content")
    if elem is None:
        sys.exit("Element with ID 'main-content' not found.")

    # 3️⃣ Read HTML text
    print("🗒️  Inner text:", elem.text_content())

    # 4️⃣ Set a new attribute
    elem.set("data-modified", "true")
    print("✅  data-modified attribute set to:", elem.get("data-modified"))

    # 5️⃣ Change background colour HTML
    elem.set("style", "background:#f0f0f0")
    print("🎨  Background colour changed to #f0f0f0")

    # 6️⃣ Write the modified HTML back to disk
    output_path = pathlib.Path("YOUR_DIRECTORY/sample_modified.html")
    output_path.write_text(html.tostring(doc, pretty_print=True, encoding="unicode"))
    print(f"💾  Modified file saved as {output_path}")

if __name__ == "__main__":
    main()
```

### ما يفعله السكربت، سطرًا بسطر

1. **Imports** `lxml.html` للتحليل و`pathlib` للمسارات المستقلة عن نظام التشغيل.  
2. **Loads** `sample.html` ويتوقف بخطأ واضح إذا كان الملف مفقوداً.  
3. **Retrieves** العنصر باستخدام **get element by id**.  
4. **Prints** نص العنصر—مُظهرًا **how to read HTML text**.  
5. **Adds** سمة مخصصة، موضحًا **how to set HTML attribute**.  
6. **Changes** لون الخلفية، مُنفّذًا متطلب **change background colour html**.  
7. **Writes** العلامات المحدثة إلى `sample_modified.html`، لتتمكن من فتحها في المتصفح ورؤية التغييرات.

تشغيل السكربت ينتج مخرجات على وحدة التحكم مشابهة لـ:

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

افتح `sample_modified.html` وستلاحظ الخلفية الرمادية خلف النص—دليل على أن **manipulate HTML with python** يعمل فعلاً.

## الأخطاء الشائعة وكيفية تجنبها

- **Missing ID** – إذا لم يكن العنصر المستهدف موجوداً، تُعيد `get_element_by_id` القيمة `None`. تحقق دائماً من `None` قبل الوصول إلى الخصائص؛ وإلا ستحصل على `AttributeError`.  
- **Encoding issues** – عند قراءة صفحات غير ASCII، مرّر `encoding='utf-8'` إلى `html.parse` أو تأكد من حفظ ملفك بـ UTF‑8.  
- **Overwriting existing styles** – تعيين سمة `style` يستبدل أي أنماط مضمّنة سابقة. إذا كنت بحاجة للحفاظ على القواعد الحالية، اقرأ قيمة `style` الحالية أولاً، أضف القاعدة الجديدة، ثم أعد كتابتها.  
- **File permissions** – الكتابة إلى نفس المجلد قد تفشل على الأنظمة ذات الصلاحيات للقراءة فقط. اختر مسار إخراج قابل للكتابة، كما فعلنا مع `sample_modified.html`.

## توسيع المثال

الآن بعد أن أتقنت الأساسيات، فكر في الخطوات التالية:

- **Loop over multiple IDs** – استخدم قائمة من المعرفات وكررها بحلقة `for` لمعالجة دفعات من أقسام الصفحة.  
- **Replace text content** – استدعِ `elem.text = "New text"` لتغيير السلسلة الظاهرة.  
- **Add child elements** – Use `

## ما الذي يجب أن تتعلمه بعد ذلك؟

- [كيفية تحرير HTML باستخدام Aspose.HTML للـ Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [كيفية استعلام HTML في Java – دليل كامل](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [كيفية تحويل HTML إلى PDF في Java – باستخدام Aspose.HTML للـ Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}