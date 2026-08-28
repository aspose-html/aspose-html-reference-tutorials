---
category: general
date: 2026-06-16
description: كيفية تغيير حجم SVG في بايثون بسرعة – تحميل ملف SVG بايثون، تعديل ملف
  SVG بايثون، وحتى تغيير حجم ملفات SVG دفعةً واحدةً باستخدام سكريبت صغير.
draft: false
keywords:
- how to resize svg
- batch resize svg files
- load svg file python
- edit svg file python
language: ar
og_description: كيف تُعيد تحجيم SVG في بايثون؟ تعلّم كيفية تحميل ملف SVG في بايثون،
  تعديل ملف SVG في بايثون، وتغيير حجم ملفات SVG دفعيًا باستخدام مثال واضح وقابل للتنفيذ.
og_title: كيفية تغيير حجم SVG في بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  headline: How to Resize SVG in Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  name: How to Resize SVG in Python – Step‑by‑Step Guide
  steps:
  - name: '**Collects** every `.svg` file in the source folder.'
    text: '**Collects** every `.svg` file in the source folder.'
  - name: '**Loads** each file using the same routine we used for a single SVG.'
    text: '**Loads** each file using the same routine we used for a single SVG.'
  - name: '**Resizes** to the desired width while keeping the aspect ratio.'
    text: '**Resizes** to the desired width while keeping the aspect ratio.'
  - name: '**Writes** the result to a new folder, leaving originals untouched.'
    text: '**Writes** the result to a new folder, leaving originals untouched.'
  type: HowTo
tags:
- Python
- SVG
- Automation
title: كيفية تغيير حجم SVG في بايثون – دليل خطوة بخطوة
url: /ar/python/general/how-to-resize-svg-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تغيير حجم SVG في بايثون – دليل شامل

هل تساءلت يومًا **كيف تغير حجم SVG** دون فتح محرر رسومات؟ ربما لديك شعار يحتاج إلى أن يكون عرضه 200 بكسل لافتة ويب، أو أنك تُعد عشرات الأيقونات لتطبيق جوال. الخبر السار؟ يمكنك القيام بذلك كله في بايثون—بدون فوتوشوب، بدون واجهة إنكسكيب، فقط بضع أسطر من الشيفرة.

في هذا الدليل سنستعرض تحميل ملف SVG في بايثون، تعديل أبعاده، وحتى تغيير حجم مجلد كامل من ملفات SVG دفعة واحدة. في النهاية ستتمكن من **load SVG file Python**، **edit SVG file Python**، و**batch resize SVG files** بثقة.

## المتطلبات المسبقة

- Python 3.8+ مثبت (أمر `python` القياسي يعمل)
- مكتبة `svgwrite` أو `lxml` – سنستخدم `lxml` لأنها توفر وصولًا مباشرًا إلى DOM.
- مجلد يحتوي على ملفات SVG تريد تغيير حجمها (مثال: `assets/icons/`)

لا تحتاج إلى أي أدوات رسومية؛ كل شيء يُنفّذ من الطرفية.

---

## الخطوة 1: تثبيت المكتبة المطلوبة

أولًا، احصل على `lxml` من PyPI. إنها صغيرة، سريعة، وتتيح لنا تعديل خصائص XML مباشرة.

```bash
pip install lxml
```

> **نصيحة احترافية:** إذا كنت تعمل في بيئة افتراضية، فعّلها قبل تشغيل الأمر. هذا يحافظ على نظافة تبعيات مشروعك.

## الخطوة 2: تحميل ملف SVG في بايثون

الآن سنقوم **load SVG file Python**—قراءة XML، الحصول على عنصر الجذر `<svg>`، وطباعة حجمه الحالي.

```python
from lxml import etree

def load_svg(path: str) -> etree._ElementTree:
    """
    Load an SVG document and return the parsed XML tree.
    """
    parser = etree.XMLParser(remove_blank_text=True)
    tree = etree.parse(path, parser)
    return tree

# Example usage
svg_path = "assets/logo.svg"
svg_tree = load_svg(svg_path)
root = svg_tree.getroot()
print(f"Original width: {root.get('width')}, height: {root.get('height')}")
```

**لماذا هذا مهم:** `lxml` يمنحنا DOM حقيقي، لذا يمكننا الاستعلام أو تعديل أي خاصية—مثالي لمهام **edit SVG file Python**.

## الخطوة 3: تغيير العرض (والارتفاع) – كيفية تغيير حجم SVG

ملفات SVG هي رسومات متجهة، لذا يمكنك ضبط العرض أو الارتفاع أو كليهما. إذا غيرت العرض فقط، سيحافظ viewBox على نسبة الأبعاد، لكن العديد من الأدوات تحترم أيضًا خاصية الارتفاع المتطابقة. إليك دالة مساعدة تعيد الحجم مع الحفاظ على نسبة الأبعاد الأصلية:

```python
def resize_svg(tree: etree._ElementTree, new_width: int) -> None:
    """
    Resize the root <svg> element to `new_width` while preserving aspect ratio.
    """
    root = tree.getroot()
    # Grab original dimensions (they may be in px, pt, or just numbers)
    orig_width = float(root.get("width").replace("px", ""))
    orig_height = float(root.get("height").replace("px", ""))

    # Compute scale factor and new height
    scale = new_width / orig_width
    new_height = round(orig_height * scale, 2)

    # Update attributes
    root.set("width", f"{new_width}px")
    root.set("height", f"{new_height}px")

    # Optional: ensure viewBox exists for better scaling in browsers
    if "viewBox" not in root.attrib:
        viewbox = f"0 0 {orig_width} {orig_height}"
        root.set("viewBox", viewbox)

# Resize to 200 px wide
resize_svg(svg_tree, 200)
```

الدالة أعلاه هي جوهر **how to resize SVG**. فهي تقرأ الحجم الحالي، تحسب ارتفاعًا متناسبًا، وتكتب الخصائص الجديدة إلى الملف.

## الخطوة 4: حفظ ملف SVG المعدل

بعد التعديل، تحتاج إلى كتابة التغييرات إلى القرص. هذا يُكمل دورة **edit SVG file Python**.

```python
def save_svg(tree: etree._ElementTree, destination: str) -> None:
    """
    Write the modified SVG tree to `destination`.
    """
    tree.write(
        destination,
        pretty_print=True,
        xml_declaration=True,
        encoding="UTF-8"
    )
    print(f"Saved resized SVG to {destination}")

# Save as a new file so the original stays untouched
output_path = "assets/logo_resized.svg"
save_svg(svg_tree, output_path)
```

شغّل السكربت بالكامل وستحصل على `logo_resized.svg` بعرض 200 بكسل بالضبط.

## الخطوة 5: تغيير حجم ملفات SVG دفعةً – معالجة مجلد كامل

الآن بعد أن استطعنا **load SVG file Python**، **edit SVG file Python**، وحفظه، لنُطبق نفس التحويل على كل ملف داخل دليل. هذا هو الجواب على **batch resize SVG files**.

```python
import pathlib

def batch_resize(source_dir: str, target_dir: str, width: int) -> None:
    """
    Resize every .svg file in `source_dir` to `width` pixels and store
    the results in `target_dir`.
    """
    src = pathlib.Path(source_dir)
    tgt = pathlib.Path(target_dir)
    tgt.mkdir(parents=True, exist_ok=True)

    svg_files = list(src.glob("*.svg"))
    if not svg_files:
        print("No SVG files found.")
        return

    for svg_path in svg_files:
        try:
            tree = load_svg(str(svg_path))
            resize_svg(tree, width)
            out_path = tgt / svg_path.name
            save_svg(tree, str(out_path))
        except Exception as e:
            print(f"Failed on {svg_path.name}: {e}")

# Example: resize everything in 'assets/icons' to 64 px wide
batch_resize("assets/icons", "assets/icons_resized", 64)
```

### ما يفعله هذا السكربت:

1. **يجمع** كل ملف `.svg` في المجلد المصدر.
2. **يحمّل** كل ملف باستخدام الروتين نفسه الذي استخدمناه للملف الفردي.
3. **يغيّر الحجم** إلى العرض المطلوب مع الحفاظ على نسبة الأبعاد.
4. **يكتب** النتيجة إلى مجلد جديد، تاركًا الأصلي دون تعديل.

الآن لديك خط أنابيب جاهز للاستخدام لـ **batch resize SVG files**.

## الخطوة 6: الحالات الخاصة والمشكلات الشائعة

| المشكلة | السبب | الحل |
|-------|--------|------|
| عدم وجود خصائص `width`/`height` | بعض ملفات SVG تعتمد فقط على `viewBox`. | إذا كانت الخصائص غائبة، استخدم أبعاد viewBox (`viewBox="0 0 w h"`). |
| وحدات غير `px` (مثل `pt`، `%`) | السكربت يزيل فقط `px`. | وسّع استدعاء `replace` أو استخدم تعبيرًا نمطيًا لالتقاط أي وحدة. |
| عناصر `<symbol>` أو `<use>` المعقدة | تغيير حجم الجذر قد لا يؤثر على الرموز المتداخلة. | طبق نفس تغييرات الخصائص على كل وسم `<symbol>`، أو استخدم CSS `transform: scale()`. |
| أحرف يونيكود أو خاصة في أسماء الملفات | `pathlib` يتعامل مع معظم الحالات، لكن Windows قد يواجه مشاكل مع بعض الأحرف. | تأكد من أن أسماء الملفات صالحة UTF‑8، أو أعد تسميتها قبل المعالجة. |

معالجة هذه القضايا مسبقًا توفر عليك مفاجآت الأيقونات المكسورة لاحقًا.

## الخطوة 7: التحقق من النتيجة

يمكنك إجراء فحص سريع باستخدام قطعة HTML صغيرة:

```html
<!DOCTYPE html>
<html>
<head><title>SVG Test</title></head>
<body>
  <h3>Original</h3>
  <img src="assets/logo.svg" alt="original logo">
  <h3>Resized</h3>
  <img src="assets/logo_resized.svg" alt="resized logo">
</body>
</html>
```

افتح الملف في المتصفح—يجب أن تبدو الصورتان متطابقتين، لكن الصورة المُعدلة ستظهر عرضًا **200 px** في أدوات المطور.

---

## الخلاصة

أصبحت الآن تعرف **how to resize SVG** باستخدام بايثون خالص، من ملف واحد إلى مجلد كامل. يغطي سير العمل **load SVG file Python**، **edit SVG file Python**، و**batch resize SVG files**—كل ذلك ببضع دوال فقط.

جرّبها: غيّر العرض، جرب تعديل الارتفاع فقط، أو أضف واجهة سطر أوامر باستخدام `argparse`. الاحتمالات لا حصر لها، والسكريبت خفيف بما يكفي لتضمينه في خطوط بناء، وظائف CI، أو أدوات سطح المكتب.

هل لديك أسئلة حول التعامل مع التدرجات اللونية، الخطوط المدمجة، أو دمج هذا في تطبيق Flask؟ اترك تعليقًا، وسنستكشف تلك الجوانب معًا. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تحويل SVG إلى صورة باستخدام Aspose.HTML في .NET](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [تحويل SVG إلى PDF باستخدام Aspose.HTML في .NET](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-pdf/)
- [عرض مستند SVG كـ PNG باستخدام Aspose.HTML في .NET](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}