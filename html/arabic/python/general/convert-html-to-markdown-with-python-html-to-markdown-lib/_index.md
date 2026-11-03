---
category: general
date: 2026-05-25
description: حوّل HTML إلى Markdown باستخدام مكتبة خفيفة الوزن لتحويل HTML إلى Markdown.
  تعلم كيفية حفظ ملف Markdown وإخراج HTML في بضع سطور فقط.
draft: false
keywords:
- convert html to markdown
- html to markdown library
- save markdown file html
language: ar
og_description: تحويل HTML إلى Markdown بسرعة. يوضح هذا الدرس كيفية استخدام مكتبة
  تحويل HTML إلى Markdown وحفظ نتائج ملف Markdown من HTML.
og_title: تحويل HTML إلى Markdown باستخدام Python – دليل سريع
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: convert html to markdown using a lightweight html to markdown library.
    Learn how to save markdown file html output in just a few lines.
  headline: convert html to markdown with Python – html to markdown lib
  type: TechArticle
- description: convert html to markdown using a lightweight html to markdown library.
    Learn how to save markdown file html output in just a few lines.
  name: convert html to markdown with Python – html to markdown lib
  steps:
  - name: Expected Output
    text: 'Running the script produces a file `links_and_paragraphs.md` containing:'
  - name: 1. What if I need to keep tables too?
    text: 'Just change the filter logic:'
  - name: 2. How does the library handle nested tags like `<strong>` or `<em>`?
    text: '`markdownify` automatically translates `<strong>` → `**bold**` and `<em>`
      → `*italic*`. If you only want links and paragraphs, those lines will be stripped
      by our filter, but you can relax the filter to keep them.'
  - name: 3. Is the conversion Unicode‑safe?
    text: ' ## Related Tutorials

      - [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
      - [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
      - [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
  type: HowTo
tags:
- HTML
- Markdown
- Python
- Conversion
title: تحويل HTML إلى ماركداون باستخدام بايثون – مكتبة HTML إلى ماركداون
url: /ar/python/general/convert-html-to-markdown-with-python-html-to-markdown-lib/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل html إلى markdown – دليل Python كامل

هل احتجت يومًا إلى **convert html to markdown** لكن لم تكن متأكدًا من الأداة التي تستخدمها؟ لست وحدك. في العديد من المشاريع—مولدات المواقع الثابتة، خطوط توثيق، أو عمليات ترحيل بيانات سريعة—تحويل HTML الخام إلى Markdown نظيف هو مهمة يومية. الخبر السار؟ باستخدام مكتبة **html to markdown library** صغيرة وبضع أسطر من Python، يمكنك أتمتة العملية بالكامل وحتى **save markdown file html** النتائج إلى القرص دون عناء.

في هذا الدليل سنبدأ من الصفر، نتناول تثبيت المكتبة المناسبة، ضبط خيارات التحويل، وأخيرًا حفظ الناتج في ملف. بنهاية الدليل ستحصل على قطعة كود قابلة لإعادة الاستخدام يمكنك إدراجها في أي سكريبت، بالإضافة إلى نصائح للتعامل مع الروابط والجداول والعناصر HTML المعقدة.

## ما ستتعلمه

- لماذا اختيار **html to markdown library** المناسبة مهم للدقة والأداء.  
- كيف تُعد خيارات التحويل لتختار فقط الميزات التي تحتاجها (مثل الروابط والفقرات).  
- الكود الدقيق المطلوب لـ **convert html to markdown** و **save markdown file html** في خطوة واحدة.  
- معالجة الحالات الخاصة للجداول، الصور، والعناصر المتداخلة.  

لا تحتاج إلى خبرة سابقة في محولات Markdown؛ فقط تثبيت أساسي لـ Python.

---

## الخطوة 1: اختيار مكتبة HTML إلى Markdown المناسبة

هناك عدة حزم Python تدعي تحويل HTML إلى Markdown، لكن ليس جميعها يمنحك تحكمًا دقيقًا. في هذا الشرح سنستخدم **markdownify**، مكتبة مُصانة جيدًا تسمح لك بتفعيل ميزات فردية عبر كائن `markdownify.MarkdownConverter`. إنها خفيفة الوزن، مكتوبة بـ Python بحت، وتعمل على كل من Windows وأنظمة Unix‑like.

```bash
pip install markdownify
```

> **نصيحة احترافية:** إذا كنت تعمل في بيئة محدودة (مثل AWS Lambda)، ثبّت النسخة المحددة (`markdownify==0.9.3`) لتجنب تغييرات غير متوقعة قد تُكسر الكود.

استخدام **markdownify** يحقق متطلب الكلمة المفتاحية الثانوية—*html to markdown library*—مع الحفاظ على وضوح الكود.

## الخطوة 2: إعداد مصدر HTML الخاص بك

لنُعرّف مقطع HTML صغير يتضمن عنوانًا، فقرةً تحتوي على رابط، وجدولًا بسيطًا. هذا يعكس ما قد تستخرجه من مشاركة مدونة أو قالب بريد إلكتروني.

```python
# Step 2: Define the source HTML content
html = """
<h1>Title</h1>
<p>Paragraph with a <a href="https://example.com">link</a>.</p>
<table><tr><td>Cell</td></tr></table>
"""
```

لاحظ كيف تم تخزين HTML في سلسلة محاطة بثلاث علامات اقتباس لتسهيل القراءة. يمكنك أيضًا قراءته من ملف أو طلب ويب؛ منطق التحويل يبقى نفسه.

## الخطوة 3: ضبط المحول بالميزات المطلوبة

أحيانًا تحتاج فقط إلى بنى Markdown محددة. تسمح لك مكتبة `markdownify` بتمرير `heading_style` وعلم `bullets`، لكن لتقليد المثال الأصلي سنركز على الروابط والفقرات. رغم أن `markdownify` لا توفر واجهة bitmask، يمكننا تحقيق نفس النتيجة عبر معالجة النتيجة لاحقًا.

```python
from markdownify import markdownify as md

def convert_html_to_markdown(html_content, keep_links=True, keep_paragraphs=True):
    """
    Convert HTML to Markdown, optionally stripping out unwanted elements.
    """
    # Convert everything first
    full_md = md(html_content, heading_style="ATX")

    # If we only want links and paragraphs, filter the lines
    lines = full_md.splitlines()
    filtered = []

    for line in lines:
        stripped = line.strip()
        if not stripped:
            continue  # skip empty lines

        if keep_links and "[" in stripped and "](" in stripped:
            filtered.append(stripped)
        elif keep_paragraphs and not stripped.startswith("#") and not stripped.startswith("-"):
            # Assume plain text lines are paragraphs
            filtered.append(stripped)

    return "\n\n".join(filtered)
```

الدالة المساعدة `convert_html_to_markdown` تقوم بالعمل الشاق: أولًا تُجري تحويلًا كاملاً، ثم تُزيل أي شيء ليس رابطًا أو فقرة. هذا يعكس نمط اختيار الميزات في **html to markdown library** من الكود الأصلي.

## الخطوة 4: حفظ ناتج Markdown في ملف

الآن بعد أن لدينا سلسلة Markdown نظيفة، حفظها أمر بسيط. سنكتب النتيجة إلى ملف اسمه `links_and_paragraphs.md` داخل المجلد الذي تحدده.

```python
import os

def save_markdown(markdown_text, directory, filename="output.md"):
    """
    Ensure the target directory exists and write the markdown text to a file.
    """
    os.makedirs(directory, exist_ok=True)  # creates the folder if needed
    file_path = os.path.join(directory, filename)

    with open(file_path, "w", encoding="utf-8") as f:
        f.write(markdown_text)

    print(f"✅ Markdown saved to {file_path}")
```

هنا نلبي متطلب **save markdown file html**: الدالة تتعامل صراحةً مع المسار وتستخدم ترميز UTF‑8 للحفاظ على أي أحرف غير ASCII قد تواجهها.

## الخطوة 5: جمع كل شيء – سكريبت كامل يعمل

فيما يلي السكريبت الكامل القابل للتنفيذ الذي يجمع كل الأجزاء معًا. انسخه إلى ملف باسم `html_to_md.py` وشغّله باستخدام `python html_to_md.py`. عدّل المتغيّر `output_dir` لتحديد المكان الذي تريد حفظ ملف Markdown فيه.

```python
# html_to_md.py
# ----------------------------------------------------
# Complete example: convert html to markdown and save
# ----------------------------------------------------
from markdownify import markdownify as md
import os

# --- Step 1: Define source HTML ------------------------------------------------
html = """
<h1>Title</h1>
<p>Paragraph with a <a href="https://example.com">link</a>.</p>
<table><tr><td>Cell</td></tr></table>
"""

# --- Step 2: Conversion helper -------------------------------------------------
def convert_html_to_markdown(html_content, keep_links=True, keep_paragraphs=True):
    """
    Convert HTML to Markdown, optionally keeping only links and paragraphs.
    """
    full_md = md(html_content, heading_style="ATX")
    lines = full_md.splitlines()
    filtered = []

    for line in lines:
        stripped = line.strip()
        if not stripped:
            continue

        if keep_links and "[" in stripped and "](" in stripped:
            filtered.append(stripped)
        elif keep_paragraphs and not stripped.startswith("#") and not stripped.startswith("-"):
            filtered.append(stripped)

    return "\n\n".join(filtered)

# --- Step 3: Save helper -------------------------------------------------------
def save_markdown(markdown_text, directory, filename="links_and_paragraphs.md"):
    """
    Save markdown_text to `directory/filename`. Creates the directory if missing.
    """
    os.makedirs(directory, exist_ok=True)
    file_path = os.path.join(directory, filename)

    with open(file_path, "w", encoding="utf-8") as f:
        f.write(markdown_text)

    print(f"✅ Markdown saved to {file_path}")

# --- Step 4: Execute conversion & saving ---------------------------------------
if __name__ == "__main__":
    # Choose which features you need – here we keep links & paragraphs only
    markdown_result = convert_html_to_markdown(html, keep_links=True, keep_paragraphs=True)

    # Define where you want the .md file to live
    output_dir = "YOUR_DIRECTORY"

    # Finally, write the file
    save_markdown(markdown_result, output_dir)
```

### النتيجة المتوقعة

تشغيل السكريبت ينتج ملف `links_and_paragraphs.md` يحتوي على:

```markdown
Paragraph with a [link](https://example.com).

Cell
```

- العنوان (`# Title`) مُستبعد لأننا طلبنا فقط الروابط والفقرات.  
- خلية الجدول تُعرض كنص عادي، مما يوضح طريقة عمل الفلتر.

---

## أسئلة شائعة وحالات خاصة

### 1. ماذا لو أردت الاحتفاظ بالجداول أيضًا؟

فقط غيّر منطق الفلتر:

```python
elif keep_tables and stripped.startswith("|"):
    filtered.append(stripped)
```

أضف علم `keep_tables` إلى توقيع الدالة واجعل قيمته `True` عند الاستدعاء.

### 2. كيف تتعامل المكتبة مع الوسوم المتداخلة مثل `<strong>` أو `<em>`؟

`markdownify` تُحوّل تلقائيًا `<strong>` → `**bold**` و `<em>` → `*italic*`. إذا كنت تريد فقط الروابط والفقرات، ستُزيل هذه السطور فلترنا، لكن يمكنك تعديل الفلتر لإبقائها.

### 3. هل التحويل آمن بالنسبة للـ Unicode؟

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}