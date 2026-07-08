---
category: general
date: 2026-07-02
description: أنشئ مستند SVG بسرعة باستخدام بايثون. تعلّم كيفية حفظ ملف SVG، وإنشاء
  صورة SVG أساسية، وتصدير SVG من الشيفرة في بضع سطور فقط.
draft: false
keywords:
- create svg document
- save svg file
- how to generate svg
- export svg from code
- create basic svg image
language: ar
og_description: أنشئ مستند SVG بسهولة. يوضح هذا الدليل كيفية إنشاء SVG، حفظ ملف SVG،
  وتصدير SVG من الكود باستخدام مثال بايثون نظيف.
og_title: إنشاء مستند SVG – دليل بايثون سريع
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  headline: Create SVG Document – Step‑by‑Step Guide for Beginners
  type: TechArticle
- description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  name: Create SVG Document – Step‑by‑Step Guide for Beginners
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: How can I add text or other shapes?
    text: Just call `svg.create_element("text", {...})` or `svg.create_element("circle",
      {...})` and append them just like the rectangle. The same **how to generate
      SVG** logic applies.
  - name: What if I need to **export SVG from code** with a transparent background?
    text: Remove any `fill` attribute from the root `<svg>` element or set `fill="none"`
      on shapes that should be transparent. The XML stays valid; browsers will render
      the transparency automatically.
  - name: Can I **save SVG file** with pretty‑printed formatting?
    text: '`ElementTree` writes compact XML by default. For a human‑readable version,
      you can use `xml.dom.minidom` to re‑format:'
  - name: What about performance for large SVGs?
    text: When generating thousands of elements, consider building a list of `ET.Element`
      objects first and then extending the root in one go. This reduces the number
      of tree mutations and speeds up the **save SVG file** operation.
  type: HowTo
tags:
- SVG
- Python
- Graphics
- File I/O
title: إنشاء مستند SVG – دليل خطوة بخطوة للمبتدئين
url: /ar/python/general/create-svg-document-step-by-step-guide-for-beginners/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند SVG – دليل خطوة بخطوة للمبتدئين

هل تساءلت يومًا كيف **تنشئ مستند SVG** دون فتح محرر رسومات؟ لست وحدك. سواء كنت تحتاج إلى أيقونة صغيرة لصفحة ويب أو مخطط ديناميكي يُولد في الوقت الفعلي، فإن القدرة على **إنشاء مستند SVG** برمجيًا توفر الوقت وتبقي كل شيء تحت التحكم بالإصدارات.

في هذا الدرس سنستعرض مثالًا كاملاً قابلًا للتنفيذ يوضح لك بالضبط كيف **تنشئ مستند SVG**، **تحفظ ملف SVG**، وحتى تجيب على سؤال “**كيف تُولد SVG**” الذي يظهر عندما تقوم بأتمتة الرسومات. في النهاية ستحصل على مربع أحمر على القرص، وستعرف كيف **تصدّر SVG من الشيفرة** لأي مشروع مستقبلي.

## ما ستحتاجه

قبل أن نغوص، تأكد من توفر التالي:

* Python 3.9 أو أحدث (المكتبة القياسية تقوم بكل العمل الشاق)
* محرر نصوص أو بيئة تطوير تحبها—VS Code، PyCharm، أو حتى Notepad يكفي
* صلاحية كتابة في مجلد ستحـــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــ​** 

## الخطوة 1: إعداد وظائف المساعدة لـ SVG (إنشاء المستند)

أولًا وقبل كل شيء: نحتاج إلى أداة مساعدة صغيرة تبني بنية XML خلف SVG. فكر فيها كالقماش الذي سنــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــــ​**  
```python
import pathlib
import xml.etree.ElementTree as ET

# ----------------------------------------------------------------------
# Helper class that mimics a minimal SVG library.
# ----------------------------------------------------------------------
class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        # Register the SVG namespace so the output looks clean
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        """Create an SVG element with the given attributes."""
        return ET.Element(tag, attrib=attributes)
    
    def append_child(self, element: ET.Element):
        """Append a child element to the root <svg> node."""
        self.root.append(element)
    
    def save(self, file_path: str):
        """Write the SVG XML to a file, creating directories as needed."""
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)
```

**لماذا هذه الخطوة مهمة:** فئة `SVGDocument` تُجرد التعامل مع XML منخفض المستوى. من خلال تغليفها في فئة نُحافظ على نظافة باقي الشيفرة، وهو ما يُعد من أفضل الممارسات عندما **تُصدّر SVG من الشيفرة** في تطبيقات أكبر.

## الخطوة 2: إضافة مستطيل – جوهر مثال **إنشاء صورة SVG أساسية**

الآن بعد أن لدينا كائن المستند، لنضيف مربعًا أحمر. هذا هو قلب جزء **إنشاء صورة SVG أساسية** من الدرس.

```python
# ----------------------------------------------------------------------
# Step 2: Build the SVG content
# ----------------------------------------------------------------------
svg = SVGDocument(width=120, height=120)   # canvas size a little larger than the square

# Define rectangle attributes: 100x100 size, red fill, positioned at (10,10)
rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}

# Create the <rect> element and attach it to the SVG root
rect_element = svg.create_element("rect", rect_attrs)
svg.append_child(rect_element)
```

**شرح:**  
* إحداثيات `x` و `y` للمستطيل تُعطيه هامشًا قدره 10 بكسل حتى لا يلتصق بالحافة.  
* استخدام قاموس للخصائص يجعل الشيفرة مقروءة ويعكس طريقة **حفظ ملف SVG** للخصائص في أي تنسيق مبني على XML.  
* إذا احتجت يومًا ما إلى **كيفية توليد SVG** لأشكال غير المستطيلات، فقط غيّر الوسم إلى `"circle"` أو `"path"` وعدّل القاموس وفقًا لذلك.

## الخطوة 3: حفظ الـ SVG – أخيرًا **حفظ ملف SVG** على القرص

لقد بنينا المستند في الذاكرة؛ الآن سنكتبه إلى ملف. هذه هي اللحظة التي يتحول فيها **إنشاء مستند SVG** المجرد إلى ملف ملموس يمكنك فتحه في المتصفح.

```python
# ----------------------------------------------------------------------
# Step 3: Persist the SVG to the filesystem
# ----------------------------------------------------------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

**ما ستراه:** فتح `output/square.svg` في Chrome أو Firefox أو أي عارض يدعم SVG سيعرض مربعًا أحمر بسيطًا بحدود بيضاء رقيقة (خلفية لوحة SVG). هذا هو الدليل على أننا نجحنا في **تصدير SVG من الشيفرة**.

## البرنامج الكامل – حل بملف واحد

فيما يلي البرنامج بالكامل، جاهز للنسخ واللصق في `create_svg.py`. تشغيل `python create_svg.py` سيولد الملف الموضح أعلاه.

```python
import pathlib
import xml.etree.ElementTree as ET

class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        return ET.Element(tag, attrib=attributes)
    def append_child(self, element: ET.Element):
        self.root.append(element)
    def save(self, file_path: str):
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)

# -------------------- Build the SVG --------------------
svg = SVGDocument(width=120, height=120)

rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}
svg.append_child(svg.create_element("rect", rect_attrs))

# -------------------- Save the file --------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع:

```
✅ SVG saved! Open output/square.svg in any browser to see the red square.
```

والملف `square.svg` المُولّد يبدو هكذا (عرض مبسط):

```xml
<?xml version='1.0' encoding='utf-8'?>
<svg xmlns="http://www.w3.org/2000/svg" width="120" height="120" version="1.1">
  <rect x="10" y="10" width="100" height="100" fill="red" />
</svg>
```

فتح الملف يُظهر مربعًا أحمرًا واضحًا—تمامًا ما كنا نهدف إلى **إنشاء صورة SVG أساسية**.

## توسيع المثال – الأسئلة الشائعة

### كيف يمكنني إضافة نص أو أشكال أخرى؟

فقط استدعِ `svg.create_element("text", {...})` أو `svg.create_element("circle", {...})` وأضفها كما فعلت مع المستطيل. نفس منطق **كيفية توليد SVG** ينطبق.

### ماذا لو أردت **تصدير SVG من الشيفرة** بخلفية شفافة؟

احذف أي خاصية `fill` من عنصر `<svg>` الجذري أو عيّن `fill="none"` على الأشكال التي يجب أن تكون شفافة. يظل XML صالحًا؛ المتصفحات ستعرض الشفافية تلقائيًا.

### هل يمكنني **حفظ ملف SVG** بتنسيق منسق (pretty‑printed)؟

`ElementTree` يكتب XML مضغوطًا افتراضيًا. للحصول على نسخة قابلة للقراءة البشرية، يمكنك استخدام `xml.dom.minidom` لإعادة تنسيق:

```python
import xml.dom.minidom as minidom

def pretty_save(svg_doc, path):
    rough_string = ET.tostring(svg_doc.root, 'utf-8')
    reparsed = minidom.parseString(rough_string)
    with open(path, 'w', encoding='utf-8') as f:
        f.write(reparsed.toprettyxml(indent="  "))
```

استبدل `svg.save(output_path)` بـ `pretty_save(svg, output_path)`.

### ماذا عن الأداء عند التعامل مع SVGs ضخمة؟

عند توليد آلاف العناصر، فكر في بناء قائمة من كائنات `ET.Element` أولًا ثم أضفها إلى الجذر دفعة واحدة. هذا يقلل من عدد عمليات تعديل الشجرة ويسرّع عملية **حفظ ملف SVG**.

## نصائح احترافية ومخاطر محتملة

* **نصيحة احترافية:** استخدم دائمًا مسارات مطلقة (أو `pathlib.Path`) عند **حفظ ملف SVG**؛ المسارات النسبية قد تتعطل عندما يُشغل السكربت من دليل عمل مختلف.  
* **احذر من:** نسيان تسجيل مساحة اسم SVG. بدون `ET.register_namespace("", SVGDocument.SVG_NS)`، سيظهر بادئة `ns0` زائدة قد يفسرها بعض المتصفحات بشكل خاطئ.  
* **خطأ شائع:** خلط الأنواع بين الأعداد الصحيحة والسلاسل في قيم الخصائص. XML يتوقع سلاسل، لذا نحول كل شيء إلى `str()`—الفئة المساعدة تقوم بذلك لك، لكن إذا تجاوزتها قد تحصل على `TypeError`.  

## الخلاصة

لقد استعرضنا مثالًا كاملاً من البداية إلى النهاية يوضح كيفية **إنشاء مستند SVG**، **حفظ ملف SVG**، والإجابة على سؤال **كيفية توليد SVG**.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}