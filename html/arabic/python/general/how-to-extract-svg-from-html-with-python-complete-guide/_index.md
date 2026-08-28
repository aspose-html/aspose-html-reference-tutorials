---
category: general
date: 2026-05-31
description: تعلم كيفية استخراج SVG من HTML باستخدام بايثون. يوضح هذا الدرس خطوة بخطوة
  كيفية قراءة مستند HTML، حفظ ملفات SVG، وحفظ SVG المضمن بكفاءة.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: ar
og_description: كيفية استخراج SVG من HTML باستخدام بايثون. اتبع هذا الدليل لقراءة
  مستند HTML، حفظ ملفات SVG والتعامل مع SVG المضمن بسهولة.
og_title: كيفية استخراج SVG من HTML باستخدام Python – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: كيفية استخراج SVG من HTML باستخدام بايثون – دليل شامل
url: /ar/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج SVG من HTML باستخدام بايثون – دليل شامل

هل تساءلت يومًا **كيف تستخرج SVG** من صفحة HTML فوضوية دون أن تفقد أعصابك؟ لست وحدك. سواءً كنت تبني أداة تجريف ويب، أو خط أنابيب تصميم، أو تحتاج فقط إلى تصدير أيقونات دفعةً، فإن معرفة **كيف تستخرج SVG** هي حيلة مفيدة توفر الوقت والجهد.

في هذا البرنامج التعليمي سنوضح لك بالضبط **كيف تستخرج SVG** باستخدام مكتبة Aspose.HTML للبايثون. سنقرأ مستند HTML، نخرج كل من العلامات `<svg>` المضمنة **و** مراجع SVG الخارجية، ثم **نحفظ ملفات SVG** على القرص—كل ذلك في سكريبت منظم وقابل لإعادة الاستخدام. في النهاية ستحصل على حل جاهز للتنفيذ يمكنك تكييفه مع مشاريعك الخاصة.

> **نصيحة محترف:** إذا كنت تريد فقط نظرة سريعة على الصفحة، فإن `BeautifulSoup` يعمل أيضًا، لكن Aspose.HTML يمنحك DOM كامل، مما يجعل استخراج كل من SVG المضمنة والمرتبطة سهلًا للغاية.

## ما الذي ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

* Python 3.8+ (الكود يستخدم f‑strings، لذا الحد الأدنى هو 3.6+)
* `pip install aspose-html` – المكتبة التجارية التي تدعم تحليل HTML لدينا
* مجلد يحتوي على ملف `input.html` يضم الـ SVGs التي تريد استخراجها
* صلاحية كتابة إلى دليل الإخراج (سنسميه `YOUR_DIRECTORY`)

هذا كل شيء—لا ملفات تنفيذية إضافية، ولا متصفحات بدون رأس. بسيط، أليس كذلك؟

## الخطوة 1: قراءة مستند HTML باستخدام Aspose.HTML

أول شيء عليك فعله هو **قراءة مستند HTML** حتى تتمكن من استعراض شجرته DOM. Aspose.HTML يمنحك كائن `HTMLDocument` يتصرف مثل `document` في المتصفح.

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*لماذا هذا مهم:* بتحميل HTML إلى DOM صحيح، تتجنب مشاكل التحليل بالاعتماد على regex، وتحصل على طرق مثل `get_elements_by_tag_name` و `query_selector_all` مجانًا.

## الخطوة 2: جمع كل عناصر `<svg>` المضمنة

الـ SVG المضمنة هي تلك الكتل `<svg>…</svg>` التي توجد داخل HTML مباشرة. **لحفظ SVG المضمنة** نحتاج فقط إلى الـ outer HTML الخاص بها.

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

لاحظ أننا نضيف العلامة الخام مباشرة إلى `svg_contents`. لاحقًا سنقرر ما إذا كان كل إدخال هو علامة أو مسار ملف.

## الخطوة 3: العثور على مراجع SVG الخارجية (وسوم img و object)

العديد من الصفحات ترتبط بملفات SVG خارجية عبر `<img src="icon.svg">` أو `<object data="logo.svg">`. **لاستخراج SVG من HTML** نحتاج إلى التقاط تلك الروابط أيضًا.

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*تنبيه حالة حافة:* إذا كان مسار SVG نسبيًا، ستحتاج إلى دمجه مع المسار الأساسي لملف HTML. للبساطة نفترض أن HTML موجود بجوار ملفات SVG.

## الخطوة 4: كتابة كل SVG إلى ملف منفصل

الآن بعد أن لدينا قائمة مختلطة من سلاسل العلامات ومسارات الملفات، سنقوم بالتكرار و**حفظ ملفات SVG**. السكريبت يميز تلقائيًا بين العلامة المضمنة وإشارة إلى ملف موجود.

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**ما ستراه:** بعد انتهاء السكريبت، سيحتوي `YOUR_DIRECTORY` على ملفات مسماة `svg_0.svg`، `svg_1.svg`، … كل منها يحمل إما العلامة المضمنة الأصلية أو نسخة من الـ SVG الخارجي.

### النتيجة المتوقعة

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

إذا كان الملف المشار إليه مفقودًا، سيطبع السكريبت تحذيرًا لكنه يستمر—لذا رابط مكسور واحد لن يوقف عملية الاستخراج بأكملها.

## معالجة المشكلات الشائعة

| المشكلة | لماذا يحدث | الحل السريع |
|---------|------------|-------------|
| **عناوين URL النسبية تتعطل** | قد يكون سمة `src` هي `"../assets/icon.svg"` | استخدم `os.path.join(os.path.dirname(html_path), src)` لحل المسار. |
| **تكرار أسماء الملفات** | ملفا SVG يحملان نفس الاسم يتم الكتابة فوقهما | أضف تجزئة (hash) للمحتوى في اسم الملف (`hashlib.md5(content.encode()).hexdigest()[:8]`). |
| **SVG المضمنة الكبيرة تسبب ارتفاع الذاكرة** | تخزين كل العلامات في قائمة قبل الكتابة | قم ببث كل عنصر مباشرة إلى ملف بدلاً من التخزين المؤقت. |
| **صور غير SVG تتسرب** | بعض وسوم `<img>` تنتهي بـ `.svg?version=1` | أزل سلاسل الاستعلام قبل فحص الامتداد (`src.split('?')[0]`). |

## السكريبت الكامل الذي يمكنك نسخه‑ولصقه

فيما يلي البرنامج الكامل الجاهز للتنفيذ. احفظه باسم `extract_svg.py`، عدل `YOUR_DIRECTORY`، ثم شغّله بـ `python extract_svg.py`.

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## ملخص – كيفية استخراج SVG باختصار

* **قراءة مستند HTML** باستخدام `HTMLDocument`.
* **جمع SVG المضمنة** عبر `get_elements_by_tag_name`.
* **تحديد SVG الخارجية** باستخدام محدد CSS ينتهي بـ `.svg`.
* **حفظ كل جزء**—اكتب العلامة مباشرة إلى ملف أو انسخ الملف المشار إليه.
* **معالجة الحالات الخاصة** مثل المسارات النسبية، التكرارات، والملفات المفقودة.

هذا هو الجواب الكامل على **كيفية استخراج SVG** من صفحة HTML، موضعًا في سكريبت واحد سهل التعديل.

## ما التالي؟

الآن بعد أن أصبحت قادرًا على **استخراج SVG** بثقة، فكر في الأفكار التالية:

* **معالجة دفعات:** كرر العملية على مجلد من ملفات HTML لبناء مكتبة أيقونات.
* **تحسين:** شغّل كل SVG محفوظ عبر SVGO (محسن Node.js) لتقليل حجم الملف.
* **تحويل:** استخدم `cairosvg` أو `svglib` لتحويل SVG إلى PNG للمتصفحات القديمة.
* **استخراج بيانات التعريف:** حلل وسوم `<title>` أو `<desc>` داخل كل SVG للحصول على تسميات قابلة للبحث.

كل من هذه المواضيع يرتبط بكلماتنا المفتاحية الثانوية—**read HTML document**, **save svg files**, **save inline svg**, **extract svg from html**—لذلك ستجد الكثير لتستكشفه.

---

*تمنياتنا لك بالنجاح! إذا واجهت أي صعوبات، اترك تعليقًا أدناه أو تواصل معي على GitHub. عالم SVG واسع، لكن مع الأدوات المناسبة يصبح استخراجها أمرًا سهلًا.*

## ماذا يجب أن تتعلم بعد ذلك؟

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Rendre un document SVG au format PNG dans .NET avec Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}