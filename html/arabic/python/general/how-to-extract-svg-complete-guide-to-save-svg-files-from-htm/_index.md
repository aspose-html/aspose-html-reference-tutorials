---
category: general
date: 2026-07-21
description: كيفية استخراج SVG من HTML وحفظ ملفات SVG بسهولة. تعلم تحويل SVG في HTML،
  تنزيل SVG المضمن، وأتمتة العملية.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to extract svg
- save svg files
- convert html svg
- extract svg from html
- download inline svg
language: ar
lastmod: 2026-07-21
og_description: كيفية استخراج SVG من HTML وحفظ ملفات SVG فورًا. يوضح لك هذا الدرس
  كيفية تحويل SVG في HTML، تنزيل SVG المضمن، وأتمتة عملية الاستخراج.
og_image_alt: Diagram illustrating how to extract SVG from an HTML document and save
  SVG files
og_title: كيفية استخراج SVG – دليل خطوة بخطوة لحفظ SVG المضمن
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: How to extract SVG from HTML and save SVG files effortlessly. Learn
    to convert HTML SVG, download inline SVG, and automate the process.
  headline: How to Extract SVG – Complete Guide to Save SVG Files from HTML
  type: TechArticle
tags:
- svg
- html
- python
- web‑scraping
title: كيفية استخراج SVG – دليل شامل لحفظ ملفات SVG من HTML
url: /ar/python/general/how-to-extract-svg-complete-guide-to-save-svg-files-from-htm/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج SVG – دليل كامل لحفظ ملفات SVG من HTML

هل تساءلت يومًا **how to extract SVG** من صفحة ويب دون نسخ العلامات يدويًا؟ لست وحدك. غالبًا ما يحتاج المطورون إلى استخراج الرسومات المتجهة من صفحات HTML — سواء لإنشاء مكتبة أصول تصميم أو لمعالجة الأيقونات على دفعات. في هذا الدرس ستتعرف على طريقة سريعة وموثوقة لـ **extract SVG from HTML**، حفظ كل رسم كملف منفصل، وحتى تحويل مقتطفات SVG في HTML إلى أصول مستقلة.

سنستعرض حلًا مبنيًا على Python يعمل على أي مستند HTML حديث، يوضح لك كيفية **save SVG files**، ويشرح تفاصيل التعامل مع **download inline SVG**. في النهاية ستحصل على سكريبت جاهز للتنفيذ يحول مجلدًا من صفحات HTML إلى مجموعة من ملفات SVG النظيفة.

## المتطلبات المسبقة – ما ستحتاجه

- Python 3.8+ مثبت (يوصى بأحدث إصدار مستقر)
- حزم `beautifulsoup4` و `lxml` (`pip install beautifulsoup4 lxml`)
- دليل يحتوي على ملفات HTML التي تريد معالجتها
- إلمام أساسي بسطر الأوامر (يكفي لتشغيل سكريبت)

لا أطر ثقيلة، ولا أتمتة للمتصفح — فقط Python عادي وقليل من المكتبات المجربة جيدًا.

## الخطوة 1: تحميل مستند HTML (How to Extract SVG – Load Phase)

الأول الذي نحتاجه هو طريقة لقراءة ملف HTML إلى الذاكرة. استخدام BeautifulSoup يجعل ذلك سهلًا ويمنحنا محللًا قويًا يتعامل مع العلامات غير الصحيحة.

```python
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(file_path: Path) -> BeautifulSoup:
    """Read an HTML file and return a BeautifulSoup object."""
    html_content = file_path.read_text(encoding="utf-8")
    # 'lxml' parser is fast and tolerant of broken HTML
    return BeautifulSoup(html_content, "lxml")
```

> **Why this matters:** تحميل المستند بشكل صحيح يضمن أن كل عنصر `<svg>` — سواء كان مضمّنًا أو مدمجًا عبر `<object>` — يكون مرئيًا لمستخرجنا. تخطي هذه الخطوة أو استخدام محلل هش غالبًا ما يؤدي إلى فقدان الرسومات.

## الخطوة 2: إنشاء مستخرج SVG (Extract SVG from HTML)

الآن بعد أن أصبح لدينا مستند مُحلل، يمكننا البحث عن جميع وسوم `<svg>`. تُجرد فئة المستخرج هذه المنطق وتُعِدّ أيضًا إعلانات الفضاء الاسمي لتكون الملفات المحفوظة نظيفة.

```python
class SvgExtractor:
    """Utility to find and retrieve all inline SVG elements from a BeautifulSoup document."""

    def __init__(self, soup: BeautifulSoup):
        self.soup = soup

    def get_all_svgs(self):
        """Yield each SVG element as a string, ready to be saved."""
        for svg in self.soup.find_all("svg"):
            # Ensure the SVG has a proper XML declaration when saved
            svg_str = str(svg)
            # Some pages omit the XML namespace; add it if missing
            if 'xmlns=' not in svg_str:
                svg_str = svg_str.replace(
                    "<svg",
                    '<svg xmlns="http://www.w3.org/2000/svg"',
                    1
                )
            yield svg_str
```

> **Pro tip:** خطوة `extract svg from html` غالبًا ما تُربك المبتدئين لأن العديد من SVG المضمّنة تفتقر إلى سمة `xmlns`. إضافتها تضمن أن الأدوات اللاحقة (مثل Inkscape) تتعرف على الملف كـ SVG صالح.

## الخطوة 3: التكرار عبر SVGs وحفظ كل واحدة (Save SVG Files)

مع جاهزية المستخرج، الجزء الأخير هو التكرار على كل SVG وكتابته إلى القرص. الدالة التالية تربط كل شيء معًا وتُظهر **how to extract SVG** في سكريبت واحد قابل لإعادة الاستخدام.

```python
def save_svgs_from_html(html_path: Path, output_dir: Path):
    """Extract all SVGs from an HTML file and save them as separate .svg files."""
    soup = load_html(html_path)
    extractor = SvgExtractor(soup)

    output_dir.mkdir(parents=True, exist_ok=True)

    for index, svg_content in enumerate(extractor.get_all_svgs()):
        svg_file = output_dir / f"svg_{index}.svg"
        svg_file.write_text(svg_content, encoding="utf-8")
        print(f"Saved {svg_file}")

# Example usage
if __name__ == "__main__":
    # Adjust these paths to match your project layout
    html_file = Path("YOUR_DIRECTORY/page.html")
    destination = Path("YOUR_DIRECTORY/svg_output")
    save_svgs_from_html(html_file, destination)
```

تشغيل هذا السكريبت سيقوم بـ **download inline SVG** من `page.html` ويضعها في `svg_output/svg_0.svg`، `svg_1.svg`، وهكذا. يوضح إخراج وحدة التحكم تأكيد حفظ كل ملف، مما يمنحك تغذية راجعة فورية.

## الخطوة 4: تحويل SVG في HTML إلى ملفات مستقلة (Convert HTML SVG)

أحيانًا ما يزال markup الـ SVG الذي تستخرجه يحتوي على مراجع إلى CSS أو JavaScript خارجية لا معنى لها إلا داخل صفحة HTML الأصلية. لتحويل **HTML SVG** إلى ملف مستقل حقًا، يمكنك إزالة وسوم `<style>` وتضمين أي CSS ضروري داخل الملف.

```python
def clean_svg(svg_str: str) -> str:
    """Remove embedded <style> tags and inline CSS for a self‑contained SVG."""
    soup = BeautifulSoup(svg_str, "xml")
    # Drop <style> elements
    for style in soup.find_all("style"):
        style.decompose()
    # Inline any style attributes (simple example)
    for element in soup.find_all(True):
        if element.has_attr("style"):
            # You could parse and apply the style here; omitted for brevity
            pass
    return str(soup)

# Integrate cleaning into the saving loop
for index, raw_svg in enumerate(extractor.get_all_svgs()):
    clean_content = clean_svg(raw_svg)
    svg_file = output_dir / f"svg_{index}.svg"
    svg_file.write_text(clean_content, encoding="utf-8")
    print(f"Saved cleaned {svg_file}")
```

> **Why clean?** SVG المستقل أسهل في الفتح بمحررات المتجهات، أو تضمينه في مشاريع أخرى، أو خدمته مباشرة من CDN. هذه الخطوة تضمن أن عملية **save svg files** تنتج أصولًا تعمل فعليًا خارج سياق الصفحة الأصلية.

## الخطوة 5: معالجة الحالات الخاصة – ملفات HTML متعددة وأسماء مكررة

في عمليات الجمع الواقعية، غالبًا ما تعالج عشرات صفحات HTML. السكريبت أدناه يوسع المثال السابق ليتجول في دليل، يستخرج من كل ملف، ويتجنب تصادم أسماء الملفات عبر إضافة اسم الملف المصدر كبادئة.

```python
def batch_extract(source_dir: Path, output_dir: Path):
    """Process every .html file in source_dir and save their SVGs."""
    for html_path in source_dir.rglob("*.html"):
        page_name = html_path.stem
        page_output = output_dir / page_name
        save_svgs_from_html(html_path, page_output)

if __name__ == "__main__":
    batch_extract(Path("YOUR_DIRECTORY/html_pages"), Path("YOUR_DIRECTORY/all_svgs"))
```

الآن يمكنك **download inline SVG** من مجموعة كاملة بأمر واحد. كل صفحة تحصل على مجلد فرعي خاص بها، مما يحافظ على ترتيب الأسماء ويمنع الكتابة فوق الملفات.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | العَرَض | الحل |
|-------|----------|-----|
| فقدان سمة `xmlns` | فتح SVG المحفوظ فارغًا في المحررات | المستخرج يضيفها تلقائيًا (انظر الخطوة 2). |
| الكيانات المشفّرة (`&amp;`, `&lt;`) | ظهور أحرف مشوهة في SVG | محلل BeautifulSoup يفكّ الشيفرة؛ تأكد من الكتابة بـ UTF‑8. |
| CSS مضمّن غير مطبق | الألوان أو الخطوط تبدو خاطئة | استخدم الدالة `clean_svg` لتضمين الأنماط الحرجة، أو احتفظ بوسم `<style>` إذا لزم الأمر. |
| ملفات HTML الكبيرة تُسبب ضغطًا على الذاكرة | تعطل السكريبت مع الصفحات الضخمة | عالج الملف سطرًا بسطر أو استخدم تدفق `lxml` (`iterparse`). |

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي السكريبت الكامل الذي يمكنك نسخه ولصقه في `extract_svg.py`. يتضمن التحميل، الاستخراج، التنظيف، والمعالجة الدفعية — كل ما تحتاجه لتطبيق **how to extract SVG** بشكل موثوق.

```python
#!/usr/bin/env python3
"""
extract_svg.py – End‑to‑end solution for extracting and saving SVG files from HTML.

Features:
- Parses single or multiple HTML files.
- Normalises missing XML namespaces.
- Optionally cleans embedded CSS for standalone SVGs.
- Organises output into per‑page folders to avoid name clashes.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def load_html(file_path: Path) -> BeautifulSoup:
    html_content = file_path.read_text(encoding="utf-8")
    return BeautifulSoup(html_content, "lxml")

class SvgExtractor:
    def __init__(self, soup: BeautifulSoup):
        self.soup = soup

    def get_all_svgs(self):
        for svg in self.soup.find_all("svg"):
            svg_str = str(svg)
            if 'xmlns=' not in svg_str:
                svg_str = svg_str.replace("<svg", '<svg xmlns="http://www.w3.org/2000/svg"', 1)
            yield svg_str

def clean_svg(svg_str: str) -> str:
    soup = BeautifulSoup(svg_str, "xml")
    for style in soup.find_all("style"):
        style.decompose()
    # Additional cleaning can be added here
    return str(soup)

def save_svgs_from_html(html_path: Path, output_dir: Path, clean: bool = True):
    soup = load_html(html_path)
    extractor = SvgExtractor(soup)

    output_dir.mkdir(parents=True, exist_ok=True)

    for idx, raw_svg in enumerate(extractor.get_all_svgs()):
        content = clean_svg(raw_svg) if clean else raw_svg
        svg_file = output_dir / f"svg_{idx}.svg"
        svg_file.write_text(content, encoding="utf-8")
        print(f"Saved {svg_file}")

def batch_extract(source_dir: Path, output_dir: Path, clean: bool = True):
    for html_path in source_dir.rglob("*.html"):
        page_folder = output_dir / html_path.stem
        save_svgs_from_html(html_path, page_folder, clean)

if __name__ == "__main__":
    # Adjust these paths for your environment
    SINGLE_HTML = Path("YOUR_DIRECTORY/page.html")
    SINGLE_OUT = Path("YOUR_DIRECTORY/svg_output")
    save_svgs_from_html(SINGLE_HTML, SINGLE_OUT)

    # Uncomment to run batch mode:
    # BATCH_SRC = Path("YOUR_DIRECTORY/html_pages")
    # BATCH_OUT = Path("YOUR_DIRECTORY/all_svgs")
    # batch_extract(BATCH_SRC, BATCH_OUT)
```

**الإخراج المتوقع** (مثال على وحدة التحكم):

```
Saved YOUR_DIRECTORY/svg_output/svg_0.svg
Saved YOUR_DIRECTORY/svg_output/svg_1.svg
```

كل ملف يحتوي على SVG مُشكل بشكل صحيح يمكنك فتحه بأي محرر متجهات أو تضمينه مباشرة في صفحة ويب أخرى.

## الخلاصة

غطّينا **how to extract SVG** من HTML، **save SVG files**، وحتى **convert HTML SVG** إلى رسومات نظيفة ومستقلة. باتباع الخطوات أعلاه يمكنك أتمتة العملية.

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [حفظ مستند SVG في Aspose.HTML للـ Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg إلى png java – تحويل SVG إلى صورة باستخدام Aspose.HTML للـ Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [svg إلى pdf java – إنشاء PDF من SVG باستخدام Aspose.HTML للـ Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}