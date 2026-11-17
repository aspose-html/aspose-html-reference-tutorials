---
category: general
date: 2026-05-28
description: استخراج SVG من HTML باستخدام Python. تعلم كيفية حفظ SVG كملف، تحويل HTML
  إلى SVG، وإنشاء مستند SVG باستخدام Python مع Aspose.HTML.
draft: false
keywords:
- extract svg from html
- save svg as file
- convert html to svg
- how to export svg files
- create svg document python
language: ar
og_description: استخراج SVG من HTML باستخدام بايثون. يوضح هذا الدليل كيفية حفظ SVG
  كملف، وتحويل HTML إلى SVG، وإنشاء مستند SVG باستخدام بايثون في دقائق.
og_title: استخراج SVG من HTML باستخدام بايثون – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Extract SVG from HTML using Python. Learn how to save SVG as file,
    convert HTML to SVG, and create SVG document python with Aspose.HTML.
  headline: Extract SVG from HTML with Python – Complete Guide
  type: TechArticle
tags:
- Python
- Aspose.HTML
- SVG
title: استخراج SVG من HTML باستخدام بايثون – دليل شامل
url: /ar/python/general/extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج SVG من HTML باستخدام Python – دليل شامل

هل تساءلت يومًا كيف **استخراج SVG من HTML** دون الحاجة إلى نسخ العلامات يدويًا؟ لست وحدك—المطورون غالبًا ما يحتاجون إلى سحب الرسوم المتجهة من صفحات الويب لإعادة استخدامها، أو للتقارير، أو لتعديلات التصميم. الخبر السار هو أنه ببضع أسطر من Python ومكتبة Aspose.HTML يمكنك أتمتة العملية بالكامل، **حفظ SVG كملف**، وحتى التعامل مع كل رسم كوثيقة مستقلة.

في هذا الدرس سنستعرض كل ما تحتاجه: تحميل صفحة HTML، العثور على كل عنصر `<svg>`، استنساخه إلى مستند SVG جديد، وأخيرًا كتابة كل واحد إلى القرص. في النهاية ستعرف **كيفية تصدير ملفات SVG** بشكل موثوق، وستحصل على سكربت قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- تثبيت Python 3.8+ (أي نسخة حديثة تعمل).
- حزمة `aspose.html`. قم بتثبيتها عبر `pip install aspose-html`.
- نسخة محلية من ملف HTML الذي يحتوي على رسومات SVG التي تريد استخراجها.
- إلمام أساسي بـ Python—لا شيء معقد، فقط القدرة على تشغيل سكربت.

إذا كان كل ذلك متوفرًا، عظيم—لنبدأ.

## الخطوة 1: إعداد المشروع واستيراد Aspose.HTML

أولًا، نحتاج إلى استيراد الفئات ذات الصلة من مكتبة Aspose.HTML. يتيح لنا هذا الاستيراد الوصول إلى كل من `HTMLDocument` لتحليل الصفحة المصدر و`SVGDocument` لإنشاء ملفات SVG جديدة.

```python
# step_1_imports.py
from aspose.html import HTMLDocument, SVGDocument
import os
```

**لماذا هذا مهم:** `HTMLDocument` يحلل شجرة DOM بالكامل، مما يسمح لنا بالبحث عن وسوم `<svg>` كما يفعل المتصفح. `SVGDocument` ينشئ ملف SVG نظيف ومتوافق مع المعايير يمكنك فتحه في أي محرر متجهات. فصل الاستيراد يجعل السكربت أسهل في الاختبار—يمكنك استبدال سطر الاستيراد وتجربة مكتبات أخرى إذا احتجت ذلك.

## الخطوة 2: تحميل ملف HTML الذي يحتوي على رسومات SVG

الآن نوجه Aspose.HTML إلى الملف الموجود على القرص. يقبل مُنشئ `HTMLDocument` مسارًا أو عنوان URL، لذا يمكنك حتى تزويده بصفحة عن بُعد إذا رغبت في ذلك.

```python
# step_2_load_html.py
def load_html(file_path: str) -> HTMLDocument:
    """Loads an HTML file and returns an HTMLDocument object."""
    if not os.path.isfile(file_path):
        raise FileNotFoundError(f"HTML file not found: {file_path}")
    return HTMLDocument(file_path)

# Example usage
html_path = "YOUR_DIRECTORY/page.html"
html_doc = load_html(html_path)
```

**لماذا نتحقق من الملف أولًا:** من السهل كتابة مسار خاطئ، وقد يؤدي الفشل الصامت إلى استثناء غامض لاحقًا. من خلال رفع `FileNotFoundError` واضح، يتوقف السكربت بسرعة ويخبرك بالخطأ بالضبط.

## الخطوة 3: العثور على جميع عناصر `<svg>`

بعد تحميل المستند، يمكننا استعلام DOM للعثور على كل عنصر `<svg>`. تُعيد طريقة `get_elements_by_tag_name` مجموعة تتصرف كقائمة Python، مما يجعل التكرار بسيطًا.

```python
# step_3_find_svgs.py
def get_svg_elements(doc: HTMLDocument):
    """Returns a list of all <svg> elements in the HTML document."""
    return doc.get_elements_by_tag_name("svg")

svg_elements = get_svg_elements(html_doc)
print(f"Found {len(svg_elements)} SVG element(s) in the HTML.")
```

**ما يحدث خلف الكواليس:** تقوم Aspose.HTML بتحليل العلامات إلى شجرة، مشابهًا لما يفعله المتصفح. من خلال استهداف وسم `svg`، نتجنب جلب صيغ صور أخرى، مما يضمن أن **convert html to svg** يعني فعليًا "أخذ الأجزاء المتجهة فقط".

## الخطوة 4: تصدير كل SVG إلى ملف منفصل

هذا هو جوهر الدرس—التكرار على عقد SVG التي تم العثور عليها، استنساخها إلى كائنات `SVGDocument` جديدة، وحفظ كل واحدة على القرص. تستنسخ الدالة `clone_node(True)` العنصر *ومعها* جميع أطفاله، محافظًا على الأنماط، والتدرجات، والمجموعات المتداخلة.

```python
# step_4_export_svgs.py
def export_svgs(svg_nodes, output_dir: str):
    """Exports each SVG node to a separate .svg file."""
    os.makedirs(output_dir, exist_ok=True)
    for index, svg_node in enumerate(svg_nodes):
        # Create a new SVG document for this element
        svg_doc = SVGDocument()
        # Clone the SVG node (deep copy) into the new document's root
        svg_doc.root = svg_node.clone_node(True)
        # Build a safe filename
        file_name = f"svg_{index}.svg"
        file_path = os.path.join(output_dir, file_name)
        # Save the SVG file
        svg_doc.save(file_path)
        print(f"Saved: {file_path}")

# Example usage
output_folder = "YOUR_DIRECTORY/extracted_svgs"
export_svgs(svg_elements, output_folder)
```

**لماذا نستخدم `clone_node(True)`:** النسخة السطحية (`False`) ستحذف الأطفال مثل `<path>` أو `<defs>`، مما ينتج SVG فارغ أو معطوب. النسخة العميقة تضمن بقاء الرسم كاملًا—وهو أمر حاسم عندما تقوم لاحقًا **save svg as file** لمعالجة لاحقة.

## السكربت الكامل – استخراج بنقرة واحدة

فيما يلي السكربت الكامل الجاهز للتنفيذ الذي يجمع كل الأجزاء معًا. احفظه باسم `extract_svg_from_html.py`، استبدل `YOUR_DIRECTORY` بالمسار الفعلي، ثم شغّله عبر `python extract_svg_from_html.py`.

```python
# extract_svg_from_html.py
"""
Extract SVG from HTML with Python – Complete, runnable example.
This script loads an HTML file, finds every <svg> element, and saves each
as an independent .svg file using Aspose.HTML.
"""

from aspose.html import HTMLDocument, SVGDocument
import os
import sys

def load_html(file_path: str) -> HTMLDocument:
    if not os.path.isfile(file_path):
        raise FileNotFoundError(f"HTML file not found: {file_path}")
    return HTMLDocument(file_path)

def get_svg_elements(doc: HTMLDocument):
    return doc.get_elements_by_tag_name("svg")

def export_svgs(svg_nodes, output_dir: str):
    os.makedirs(output_dir, exist_ok=True)
    for index, svg_node in enumerate(svg_nodes):
        svg_doc = SVGDocument()
        svg_doc.root = svg_node.clone_node(True)
        file_name = f"svg_{index}.svg"
        file_path = os.path.join(output_dir, file_name)
        svg_doc.save(file_path)
        print(f"Saved: {file_path}")

def main():
    # Adjust these paths to match your environment
    html_path = "YOUR_DIRECTORY/page.html"
    output_folder = "YOUR_DIRECTORY/extracted_svgs"

    try:
        html_doc = load_html(html_path)
        svg_elements = get_svg_elements(html_doc)

        if not svg_elements:
            print("No <svg> elements found. Nothing to export.")
            sys.exit(0)

        export_svgs(svg_elements, output_folder)
        print("All SVG files have been extracted successfully.")
    except Exception as e:
        print(f"Error: {e}")

if __name__ == "__main__":
    main()
```

**الناتج المتوقع** (بافتراض وجود ثلاثة SVGs في ملف HTML المصدر):

```
Found 3 SVG element(s) in the HTML.
Saved: YOUR_DIRECTORY/extracted_svgs/svg_0.svg
Saved: YOUR_DIRECTORY/extracted_svgs/svg_1.svg
Saved: YOUR_DIRECTORY/extracted_svgs/svg_2.svg
All SVG files have been extracted successfully.
```

يمكنك الآن فتح أي من ملفات `.svg` التي تم إنشاؤها في Inkscape أو Illustrator أو حتى في المتصفح للتحقق من سلامة الرسومات.

## المشكلات الشائعة & نصائح احترافية

- **غياب المساحات الاسمية:** بعض صفحات HTML تدمج SVGs مع مساحة اسم صريحة (`xmlns="http://www.w3.org/2000/svg"`). Aspose.HTML يتعامل مع ذلك تلقائيًا، لكن إذا انتقلت إلى محلل أخف (مثل `BeautifulSoup`) سيتعين عليك الحفاظ على مساحة الاسم يدويًا.
- **CSS مدمج:** الأنماط المضمنة تُستنسخ، لكن ملفات CSS الخارجية المشار إليها عبر `<link>` لن تنتقل مع SVG. إذا احتجت تلك الأنماط، فكر في دمجها داخل المستند قبل التصدير—Aspose.HTML يوفر نسخة `Document.save` يمكنها تضمين CSS.
- **الملفات الكبيرة:** عند استخراج مئات SVGs، قد ترغب في تدفق الإخراج لتقليل استهلاك الذاكرة. النهج الحالي يحتفظ بكل SVG في الذاكرة فقط لمدة عملية الحفظ، وهو عادةً كافٍ لمعظم الحالات.
- **تصادم أسماء الملفات:** يستخدم السكربت فهرسًا بسيطًا (`svg_0.svg`). إذا شغلته عدة مرات في نفس المجلد، ستُستبدل الملفات. أضف طابعًا زمنيًا أو تجزئة إلى اسم الملف للسلامة.

## نظرة بصرية

فيما يلي مخطط سريع لتدفق البيانات—from ملف HTML المصدر إلى ملفات SVG الفردية على القرص.

![Extract SVG from HTML process diagram](https://example.com/diagram.png "Extract SVG from HTML workflow")

*نص بديل: مخطط يوضح كيفية استخراج SVG من HTML باستخدام Python و Aspose.HTML.*

## توسيع الحل

الآن بعد أن أصبحت قادرًا على **create SVG document python**، قد تتساءل عن ما يمكن عمله لاحقًا:

- **تحويل دفعي:** غلف السكربت بحلقة تمر عبر مجلد من ملفات HTML، وتجمع جميع SVGs في مجلد واحد.
- **معالجة لاحقة:** استخدم مكتبات مثل `cairosvg` لتحويل SVG المستخرجة إلى PNG أو PDF لتدفقات عمل قائمة على الرسوم النقطية.
- **إدخال بيانات وصفية:** قبل الحفظ، أضف وسوم `<desc>` أو `<metadata>` مخصصة لكل SVG لتضمين معلومات المؤلف أو رقم الإصدار.

هذه الإضافات بسيطة لأن المنطق الأساسي—استنساخ العقدة والحفظ—يبقى كما هو.

## الخلاصة

لقد أظهرنا لك كيفية **extract SVG from HTML** باستخدام سكربت Python مختصر، بدءًا من تحميل مستند HTML إلى **saving SVG as file** ومعالجة الحالات الخاصة. هذا النهج موثوق، يعمل مع أي عدد من الرسومات، ويستفيد من API القوي لـ Aspose.HTML للحفاظ على محتوى SVG بأمان.

لا تتردد في التجربة—غيّر مسار الإدخال إلى URL بعيد، عدل نظام التسمية، أو وجه الناتج إلى خط أنابيب CI يتحقق من توافق SVG. الاحتمالات لا حصر لها، والآن لديك أساس صلب للانطلاق.

هل لديك أسئلة حول **how to export SVG files** في بيئة مختلفة، أو تحتاج مساعدة في تعديل السكربت لحالة استخدام محددة؟ اترك تعليقًا أدناه، وتمنياتنا لك بالبرمجة السعيدة!

## دروس ذات صلة

- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [Convert SVG to PDF in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-pdf/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}