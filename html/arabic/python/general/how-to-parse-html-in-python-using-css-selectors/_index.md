---
category: general
date: 2026-10-21
description: تعلم كيفية تحليل HTML في بايثون، تحميل مستند HTML، استخدام محددات CSS،
  واستخراج الروابط التشعبية من HTML بسرعة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- how to use selector
- extract hyperlinks from html
- load html document python
language: ar
lastmod: 2026-10-21
og_description: كيفية تحليل HTML في بايثون باستخدام محددات CSS. تحميل مستند HTML،
  اختيار الروابط، واستخراج الروابط التشعبية من HTML بكود نظيف.
og_image_alt: Screenshot showing how to parse HTML in Python with CSS selectors
og_title: كيفية تحليل HTML في بايثون – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to parse HTML in Python, load an HTML document, use CSS selectors,
    and extract hyperlinks from HTML quickly.
  headline: How to parse HTML in Python using CSS selectors
  type: TechArticle
tags:
- python
- html-parsing
- css-selectors
title: كيفية تحليل HTML في بايثون باستخدام محددات CSS
url: /ar/python/general/how-to-parse-html-in-python-using-css-selectors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحليل HTML في Python باستخدام CSS selectors

إذا كنت بحاجة إلى **how to parse html** في سكريبت Python، فإن هذا الدليل يوضح لك ذلك بالضبط. ستتعلم كيفية تحميل مستند HTML، وكيفية استخدام صياغة selector للعثور على العناصر، وكيفية استخراج الروابط التشعبية من html دون كتابة محلل مخصص.

تحليل HTML هو مهمة شائعة لمجمعات الويب، خطوط أنابيب تحليل البيانات، أو الاختبار الآلي. بنهاية هذا الدرس ستحصل على دالة قابلة لإعادة الاستخدام تقوم بتحميل مستند HTML، وتختار جميع وسوم `<a>` باستخدام CSS selector، وتعيد قائمة نظيفة من عناوين URL.

## ما ستحتاجه

- Python 3.8+ (الكود يعمل على أي نسخة حديثة)  
- مكتبة **lxml** (`pip install lxml`) – توفر تحليل HTML سريع ودعم CSS selector  
- ملف HTML تريد تحليله (مثال، `sample.html`)  

لا توجد أدوات إضافية مطلوبة؛ كل شيء يعمل باستخدام المكتبة القياسية وحزمة طرف ثالث واحدة.

## الخطوة 1: How to parse HTML – تحميل المستند

الخطوة الأولى في أي سير عمل HTML هي قراءة الملف إلى الذاكرة. استخدام **lxml.html** يمنحك كائن شجرة يدعم CSS selectors.

```python
# step_1_load.py
from lxml import html

def load_html(path: str) -> html.HtmlElement:
    """
    Load an HTML document from the given file path.
    Returns an lxml HtmlElement that can be queried with CSS selectors.
    """
    with open(path, "r", encoding="utf-8") as f:
        content = f.read()
    # Parse the raw HTML string into a tree
    return html.fromstring(content)

# Example usage
doc = load_html("sample.html")
print("Document loaded – ready for selector queries.")
```

**لماذا هذا مهم:**  
`load_html` يُجرد تفاصيل قراءة الملف المتكررة ويضمن أن يتم تحليل المستند باستخدام محلل HTML متسامح. هذه هي الطريقة الأكثر أمانًا لـ **load html document python** دون القلق بشأن العلامات المشوهة.

## الخطوة 2: How to use selector – العثور على جميع عناصر الروابط

بمجرد تحميل المستند، يمكنك استخدام CSS selector لتحديد كل وسوم `<a>`. المحدد `"a"` يطابق جميع عناصر الارتباط، لكن يمكنك تحسينه (مثال، `"a.external"` أو `"nav a"`).

```python
# step_2_selector.py
def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    """
    Return a list of <a> elements using a CSS selector.
    This demonstrates how to use selector syntax with lxml.
    """
    # The CSS selector "a" selects every anchor tag
    return doc.cssselect("a")

# Example usage
links = select_links(doc)
print(f"Found {len(links)} <a> elements.")
```

**لماذا هذا مهم:**  
نهج **how to use selector** يتيح لك التعبير عن استعلامات معقدة في سلسلة واحدة قابلة للقراءة، متجنبًا التنقل اليدوي في الشجرة. يعمل مع أي نمط CSS يدعمه `lxml.cssselect`.

## الخطوة 3: استخراج الروابط التشعبية من HTML ومعالجتها

الآن بعد أن لديك قائمة من عناصر `<a>`، يمكنك استخراج سمة `href` من كل منها. الأداة المساعدة أدناه تقوم أيضًا بتطبيع عناوين URL النسبية مقابل عنوان أساسي (إذا قمت بتوفير واحد).

```python
# step_3_extract.py
from urllib.parse import urljoin
from typing import Optional

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    """
    Return a list of href values from the given <a> elements.
    If base_url is supplied, relative URLs are resolved to absolute URLs.
    """
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            # Skip <a> tags without an href attribute
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

# Example usage
hyperlinks = extract_hyperlinks(links, base_url="https://example.com")
for url in hyperlinks:
    print(url)
```

**الناتج المتوقع** (بافتراض أن `sample.html` يحتوي على ثلاثة روابط):

```
https://example.com/page1.html
https://example.com/page2.html
https://external.org/resource
```

**لماذا هذا مهم:**  
`extract_hyperlinks` هو جوهر **extract hyperlinks from html**. يتعامل بأناقة مع سمة `href` المفقودة، يحل الروابط النسبية، ويعيد قائمة Python عادية يمكنك تمريرها إلى معالجة إضافية (مثال، requests، pandas، أو قاعدة بيانات).

## مثال كامل من البداية إلى النهاية

دمج الدوال الثلاثة معًا يمنحك سكريبت واحد يقوم بتحميل ملف، يحدد جميع الروابط، ويطبع كل رابط تشعبي.

```python
# parse_links.py
from lxml import html
from urllib.parse import urljoin
from typing import Optional

def load_html(path: str) -> html.HtmlElement:
    with open(path, "r", encoding="utf-8") as f:
        return html.fromstring(f.read())

def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    return doc.cssselect("a")

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

if __name__ == "__main__":
    # 1️⃣ Load the HTML document
    document = load_html("sample.html")
    # 2️⃣ Use selector to grab all <a> tags
    anchor_elements = select_links(document)
    # 3️⃣ Extract and print each hyperlink
    for url in extract_hyperlinks(anchor_elements, base_url="https://example.com"):
        print(url)
```

تشغيل `python parse_links.py` يطبع كل رابط تشعبي، مُحل بالكامل، إلى وحدة التحكم. هذا السكريبت يُظهر **how to parse html**، **how to use selector**، و **extract hyperlinks from html** في تدفق واحد قابل لإعادة الاستخدام.

## تنوعات شائعة ومعالجة الحالات الطرفية

| الحالة | ما الذي يجب تغييره | السبب |
|-----------|----------------|--------|
| **فقط عناوين URL المطلقة مطلوبة** | إهمال معامل `base_url` في `extract_hyperlinks` | يترك عناوين URL النسبية دون تعديل |
| **تحتاج أيضًا إلى نص الرابط** | إرجاع زوج `(href, link.text_content())` من `extract_hyperlinks` | يسمح لك بتخزين كل من URL ونص الارتباط |
| **ملفات HTML الكبيرة** | استخدام `lxml.etree.iterparse` مع مرشح CSS selector | يقلل من استهلاك الذاكرة عن طريق البث |
| **محدد مختلف** | استبدال `"a"` بـ `"nav a[href]"` أو `"div.content a.external"` | يستهدف مجموعة فرعية من الروابط، مفيد لـ **how to use selector** في الصفحات المعقدة |

**نصيحة احترافية:** دائمًا تحقق من صحة عناوين URL المستخرجة قبل إجراء طلبات الشبكة. فحص سريع باستخدام `urlparse` يمكنه تصفية السلاسل المشوهة وحماية المجمع الخاص بك من الأعطال.

## الخلاصة

أنت الآن تعرف **how to parse html** في Python، وكيفية **load html document python**، وكيفية **how to use selector** لاستهداف العناصر، وكيفية **extract hyperlinks from html** بفعالية. المثال الكامل أعلاه جاهز للنسخ واللصق في مشروعك، ويمكنك تعديل كل دالة لتناسب حالات استخدام أكثر تقدمًا مثل الترميز الصفحات، المحتوى المُولد بواسطة JavaScript، أو الزحف متعدد الصفحات.

- استخدام **requests‑html** أو **Playwright** لجلب الصفحات التي تتطلب تنفيذ JavaScript.  
- تخزين الروابط المستخرجة في ملف CSV أو قاعدة بيانات SQLite للتحليل لاحقًا.  
- إضافة معالجة أخطاء لمهلات الشبكة ورموز حالة HTTP.

تحليل سعيد، ولا تتردد في تجربة محددات مختلفة لاكتشاف القوة الكاملة لاستعلامات HTML المعتمدة على CSS في Python!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة من الشيفرة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تكوين معالجة موارد HTML في Python وتحميل مستند HTML](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [كيفية تحليل HTML في Python – دليل كامل](/html/english/python/general/how-to-parse-html-in-python-complete-guide/)
- [كيفية تحميل HTML في Python – دليل خطوة بخطوة](/html/english/python/general/how-to-load-html-in-python-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}