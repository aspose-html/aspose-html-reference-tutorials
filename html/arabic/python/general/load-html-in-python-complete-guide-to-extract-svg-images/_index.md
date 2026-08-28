---
category: general
date: 2026-06-10
description: تحميل HTML في بايثون لاستخراج صور SVG من صفحاتك — كود خطوة بخطوة، نصائح،
  وتعامل مع الحالات الخاصة.
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: ar
og_description: حمّل HTML في بايثون واستخرج صور SVG مع مثال واضح وقابل للتنفيذ. تعلم
  كيفية البحث عن عناصر SVG في HTML وتعامل مع الحالات الخاصة.
og_title: تحميل HTML في بايثون – استخراج صور SVG بكفاءة
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML in Python to extract SVG images from your pages—step-by-step
    code, tips, and edge‑case handling.
  headline: Load HTML in Python – Complete Guide to Extract SVG Images
  type: TechArticle
tags:
- python
- html-parsing
- svg
title: تحميل HTML في بايثون – دليل شامل لاستخراج صور SVG
url: /ar/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحميل HTML في بايثون – الدليل الكامل لاستخراج صور SVG

هل احتجت يوماً إلى **تحميل HTML في بايثون** فقط لاستخراج كل رسومات SVG من صفحة؟ لست وحدك. سواء كنت تبني أداة تجريف ويب، أو تُنشئ تقرير أصول، أو مجرد فضولي حول الأيقونات التي يستخدمها موقع ما، فإن معرفة كيفية **استخراج صور SVG** توفر عليك الكثير من البحث اليدوي.

في هذا الدرس سنستعرض حلاً عملياً من البداية إلى النهاية يقوم **بتحميل HTML في بايثون**، ثم **يبحث عن عناصر SVG في HTML**، **يجد SVG المضمنة**، وحتى يلتقط ملفات SVG الخارجية المشار إليها عبر وسوم `<img>`. في النهاية ستحصل على سكريبت قابل لإعادة الاستخدام، وبعض النصائح للجزء الصعب، وصورة واضحة لما سيبدو عليه الناتج.

## ما ستحصل عليه بعد الانتهاء

* سكريبت بايثون جاهز للتنفيذ يقوم بتحليل ملف HTML محلي (أو صفحة تم جلبها) ويُدرج كل SVG يمكنه العثور عليه.  
* فهم الفرق بين **SVG المضمنة** (`<svg>…</svg>`) و **SVG الخارجية** (`<img src="… .svg">`).  
* استراتيجيات للتعامل مع العلامات غير الصحيحة، الملفات المفقودة، ومشكلات النطاقات.  
* أفكار لتوسيع الكود—حفظ ملفات SVG، تحويلها إلى PNG، أو إدخالها في قاعدة بيانات.

### المتطلبات المسبقة

* تثبيت Python 3.8+.  
* إلمام أساسي بمكتبات بايثون `requests` و `BeautifulSoup` (سنستوردها، لا حاجة لتعمق).  
* ملف HTML محلي أو عنوان URL ترغب في فحصه.  

الآن، لنبدأ.

## تحميل HTML في بايثون – إعداد المحلل

الخطوة الأولى هي **تحميل HTML في بايثون**. يمكنك إما قراءة ملف من القرص أو جلب صفحة عن بُعد. أدناه مثال مساعد بسيط لكنه قوي يقوم بالاثنين:

```python
import os
import requests
from bs4 import BeautifulSoup

def load_html(source: str) -> BeautifulSoup:
    """
    Load HTML content from a file path or a URL and return a BeautifulSoup object.
    """
    if os.path.isfile(source):
        # Load from local file
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        # Assume it's a URL and fetch it
        response = requests.get(source)
        response.raise_for_status()
        html = response.text

    # Use the html.parser for speed; switch to 'lxml' if you need extra robustness
    soup = BeautifulSoup(html, "html.parser")
    return soup
```

> **لماذا هذا مهم:** استخدام `BeautifulSoup` يُبسط التعامل مع تعقيدات تحليل النصوص الخام، وتتعامل الدالة بسلاسة مع الملفات المحلية وعناوين URL البعيدة. كما أنها تُطلق استثناءً إذا فشل طلب الشبكة—وبذلك تعرف فوراً متى حدث خطأ.

## استخراج صور SVG – العثور على عناصر SVG المضمنة

بعد تحميل المستند، الخطوة المنطقية التالية هي **العثور على وسوم SVG المضمنة**. الـ SVG المضمنة تكون مدمجة مباشرةً في شفرة HTML، مما يتيح لك التقاطها مباشرةً من الـ DOM.

```python
def collect_inline_svg(soup: BeautifulSoup) -> list:
    """
    Return a list of all inline <svg> elements as strings.
    """
    inline_svgs = []
    for svg in soup.find_all("svg"):
        # Preserve the original markup; .decode() gives us a string representation
        inline_svgs.append(str(svg))
    return inline_svgs
```

*نصيحة احترافية:* إذا استخدمت الصفحة نطاقات SVG (`<svg xmlns="http://www.w3.org/2000/svg">`)، فإن `BeautifulSoup` لا يزال يجد الوسم لأنّه يتجاهل النطاقات افتراضياً. هذا يُعدّ ميزة مريحة عندما تكون فقط **تبحث عن SVG في HTML**.

## البحث عن SVG في HTML – معالجة مراجع `<img>` الخارجية

العديد من المواقع لا تُضمّن SVG مباشرةً؛ بل تُشير إلى ملفات خارجية عبر `<img src="icon.svg">`. لالتقاط هذه الملفات، نحتاج إلى تكرار جميع وسوم `<img>`، فحص قيمة `src`، ومعرفة ما إذا كانت تنتهي بـ `.svg`.

```python
def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    """
    Return a list of file paths or URLs that point to external SVG images.
    If base_path is provided, it will be joined with relative URLs.
    """
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            # Resolve relative paths if a base directory or URL is given
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs
```

> **تحذير حالة حافة:** بعض الصفحات تستخدم سلاسل استعلام (`icon.svg?v=2`) أو شظايا (`icon.svg#layer`). لا يزال فحص `endswith(".svg")` يعمل لأننا ننظر فقط إلى الجزء الأخير من السلسلة بعد تحويلها إلى أحرف صغيرة. إذا احتجت إلى تحقق أكثر صرامة، فكر باستخدام `urllib.parse` لإزالة المعاملات أولاً.

## العثور على SVG المضمنة – تقرير النتائج

الآن بعد أن لدينا قائمتين—واحدة لعلامات SVG المضمنة وأخرى لمراجع الملفات الخارجية—يمكننا دمجهما وإبلاغ العدد الكلي. هذا يشبه المقتطف الأصلي الذي شاركته، لكنه يضيف بعض السياق الإضافي.

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## تجميع كل شيء معاً – السكريبت الكامل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. احفظه باسم `extract_svg.py` ووجهه إما إلى ملف HTML محلي أو إلى عنوان URL.

```python
#!/usr/bin/env python3
import os
import sys
import requests
from bs4 import BeautifulSoup

# -------------------------------------------------
# Helper functions (see definitions above)
# -------------------------------------------------
def load_html(source: str) -> BeautifulSoup:
    if os.path.isfile(source):
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        response = requests.get(source)
        response.raise_for_status()
        html = response.text
    return BeautifulSoup(html, "html.parser")

def collect_inline_svg(soup: BeautifulSoup) -> list:
    return [str(svg) for svg in soup.find_all("svg")]

def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs

def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")

# -------------------------------------------------
# Main execution
# -------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python extract_svg.py <path-or-url-to-html>")
        sys.exit(1)

    source = sys.argv[1]
    soup = load_html(source)

    # Determine base path for relative <img> sources (only relevant for local files)
    base_dir = os.path.dirname(os.path.abspath(source)) if os.path.isfile(source) else ""

    inline_svgs = collect_inline_svg(soup)
    external_svgs = collect_external_svg(soup, base_dir)

    report_svg_counts(inline_svgs, external_svgs)

    # Optional: write inline SVGs to separate files for inspection
    for idx, svg_markup in enumerate(inline_svgs, start=1):
        out_path = f"inline_svg_{idx}.svg"
        with open(out_path, "w", encoding="utf-8") as out_file:
            out_file.write(svg_markup)
        print(f"Saved inline SVG #{idx} to {out_path}")

    # Optional: download external SVGs (uncomment if needed)
    # for url in external_svgs:
    #     try:
    #         resp = requests.get(url)
    #         resp.raise_for_status()
    #         filename = os.path.basename(url.split("?")[0])
    #         with open(filename, "wb") as f:
    #             f.write(resp.content)
    #         print(f"Downloaded {url} → {filename}")
    #     except Exception as e:
    #         print(f"Failed to download {url}: {e}")
```

### الناتج المتوقع

تشغيل السكريبت على ملف `sample.html` تجريبي قد ينتج ما يلي:

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

إذا قمت بإلغاء التعليق عن كتلة التحميل، فإن SVG الخارجي


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُكمل التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}