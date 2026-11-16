---
category: general
date: 2026-06-26
description: تعلم كيفية الحصول على أيقونة الموقع (favicon) بتحميل HTML من عنوان URL
  واستخراج href من وسوم الرابط. كود بايثون خطوة بخطوة للحصول على أيقونات المواقع بسرعة.
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: ar
og_description: 'كيفية الحصول على أيقونة الموقع بسرعة: تحميل HTML من عنوان URL، العثور
  على وسم link rel=''icon''، واستخراج href من وسوم link باستخدام بايثون.'
og_title: كيفية الحصول على الفافيكون – دورة بايثون
schemas:
- author: Aspose
  dateModified: '2026-06-26'
  description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  headline: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  type: TechArticle
- description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  name: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  steps:
  - name: What if the site uses a `<meta>` tag instead of `<link>`?
    text: Some older pages embed the icon URL in a `<meta name="msapplication‑TileImage">`.
      You can extend `find_icon_links` to also search for those meta tags and treat
      them the same way.
  - name: How do I handle relative URLs that start with `//`?
    text: '`urljoin` automatically resolves protocol‑relative URLs (`//example.com/favicon.ico`)
      based on the scheme of the base URL, so you don’t need extra logic.'
  - name: Can I retrieve multiple sizes (e.g., 32×32, 180×180) automatically?
    text: Yes—just drop the `filter_ico_urls` step. The script will return every icon
      URL it discovers, including PNGs of various dimensions. You can then sort or
      select based on the filename pattern.
  - name: Does this work on sites that block bots?
    text: 'If a site returns a 403 or requires a custom User‑Agent, tweak the `requests.get`
      call:'
  type: HowTo
tags:
- Python
- Web Scraping
- HTML Parsing
title: كيفية الحصول على الفافيكون – دليل بايثون الكامل لاستخراج أيقونات المواقع
url: /ar/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية الحصول على أيقونة الموقع – دليل بايثون كامل لاستخراج أيقونات المواقع

هل تساءلت يومًا **كيف تحصل على أيقونة الموقع** من أي موقع ويب دون الغوص في شفرة الصفحة يدويًا؟ لست وحدك—المطورون، خبراء SEO، وحتى المصممون غالبًا ما يحتاجون إلى الأيقونة الصغيرة التي تمثل الموقع. في هذا الدرس سنظهر لك طريقة نظيفة ومركزة على بايثون لتحميل HTML من عنوان URL، وتحديد وسوم `<link rel="icon">`، واستخراج عناوين أيقونات الموقع. في النهاية، ستعرف بالضبط **كيف تحصل على أيقونة الموقع** لأي نطاق، وستحصل على سكربت قابل لإعادة الاستخدام لمشاريعك.

سنتناول كل شيء من جلب HTML إلى معالجة الحالات الخاصة مثل الروابط النسبية وتنسيقات الأيقونات المتعددة. لا حاجة لخدمات خارجية—فقط مكتبة `requests` القياسية ومحلل HTML خفيف الوزن. هل أنت مستعد للبدء؟ هيا نغوص.

## المتطلبات المسبقة

- Python 3.8+ مثبت (الكود يعمل على 3.10 أيضًا)  
- إلمام أساسي بـ `requests` وفهم list comprehensions  
- اتصال بالإنترنت للموقع المستهدف  

إذا كان لديك هذه المتطلبات بالفعل، عظيم—تجاوز إلى الخطوة الأولى. وإلا، قم بتثبيت الاعتماد الوحيد الذي نحتاجه:

```bash
pip install requests beautifulsoup4
```

> **نصيحة احترافية:** `beautifulsoup4` هو محلل تم اختباره في المعارك يجعل عملية “load html from url” سهلة للغاية.

## الخطوة 1: تحميل HTML من URL باستخدام بايثون  

أول شيء تحتاج إلى القيام به عند تعلم **كيف تحصل على أيقونة الموقع** هو جلب مصدر الصفحة. هذه هي خطوة “load html from url” في العملية.

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

لماذا نستخدم `requests`؟ فهي تتعامل مع عمليات إعادة التوجيه، والتحقق من HTTPS، والمهلات تلقائيًا، مما يعني مفاجآت أقل عندما تحاول لاحقًا **الحصول على أيقونات الموقع**.

## الخطوة 2: تحليل المستند وإيجاد روابط الأيقونات  

الآن بعد أن حصلنا على HTML، نحتاج إلى تحديد جميع عناصر `<link>` التي تشير خاصية `rel` الخاصة بها إلى أيقونة. هذا هو جوهر **كيف تحصل على أيقونة الموقع**.

```python
def find_icon_links(html: str) -> list[BeautifulSoup]:
    """Return a list of <link> tags that declare an icon."""
    soup = BeautifulSoup(html, "html.parser")
    # Look for rel="icon" or rel="shortcut icon"
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]
```

لاحظ أننا نتحقق من كل من `icon` و `shortcut icon` لأن المواقع القديمة لا تزال تستخدم الأخيرة. هذه اللمحة الصغيرة غالبًا ما تربك الأشخاص عندما يبحثون عن “how to extract favicons”.

## الخطوة 3: استخراج href من عناصر الرابط  

مع وجود الوسوم ذات الصلة، الخطوة المنطقية التالية—**استخراج href من الرابط**—هي بسيطة.

```python
from urllib.parse import urljoin

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    """Convert each <link> tag’s href into a full absolute URL."""
    urls = []
    for tag in link_tags:
        href = tag.get("href")
        if href:
            # Resolve relative URLs against the base page
            full_url = urljoin(base_url, href)
            urls.append(full_url)
    return urls
```

استخدام `urljoin` يضمن أنه حتى إذا قدم الموقع مسارًا نسبيًا مثل `/favicon.ico`، ستحصل على عنوان URL مطلق صحيح—وهو أمر حاسم لسكربت **كيف تحصل على أيقونة الموقع** موثوق.

## الخطوة 4: اختياري – التحقق وتصفية عناوين أيقونات URL  

أحيانًا تُدرج الصفحة العديد من الأيقونات (Apple touch icons، PNG بأحجام مختلفة، إلخ). إذا كنت تهتم فقط بملف `.ico` الكلاسيكي، قم بالتصفية وفقًا لذلك. تُظهر هذه الخطوة **كيفية استخراج favicons** من نوع معين.

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

لا تتردد في تعديل الفلتر: استبدل `".ico"` بـ `".png"` أو تحقق من `rel="apple-touch-icon"` إذا كنت بحاجة إلى أيقونات عالية الدقة.

## الخطوة 5: تنزيل ملفات الأيقونة (إذا كنت تريد الصورة الفعلية)  

استخراج عناوين URL هو نصف المعركة؛ التنزيل يمنحك ملفًا يمكنك عرضه أو تخزينه. إليك أداة مساعدة سريعة:

```python
import os

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    """Save each icon to *folder*, creating it if necessary."""
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")
```

تشغيل هذا بعد الخطوات السابقة يمنحك نسخة محلية من كل أيقونة تم اكتشافها، مثالي للتخزين المؤقت أو التحليل دون اتصال.

## الخطوة 6: تجميع كل شيء معًا – مثال كامل يعمل  

فيما يلي السكربت الكامل الجاهز للتنفيذ الذي يوضح **كيف تحصل على أيقونة الموقع** من أي موقع. انسخه، غير `target_url`، وشاهد النتيجة.

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
import os

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def find_icon_links(html: str) -> list[BeautifulSoup]:
    soup = BeautifulSoup(html, "html.parser")
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    return [urljoin(base_url, tag.get("href")) for tag in link_tags if tag.get("href")]

def filter_ico_urls(urls: list[str]) -> list[str]:
    return [u for u in urls if u.lower().endswith(".ico")]

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")

def get_favicons(target_url: str) -> None:
    print(f"Fetching HTML from {target_url} …")
    html = fetch_html(target_url)

    print("Finding <link> tags that declare icons …")
    icon_tags = find_icon_links(html)

    print(f"Extracting href attributes – {len(icon_tags)} candidates found.")
    raw_urls = extract_icon_urls(target_url, icon_tags)

    # Optional filtering – keep only .ico files
    ico_urls = filter_ico_urls(raw_urls)
    print(f"Filtered to {len(ico_urls)} .ico URLs:", ico_urls)

    if ico_urls:
        download_icons(ico_urls)
    else:
        print("No .ico favicons detected; here are all discovered URLs:")
        print(raw_urls)

# Example usage – replace with any site you want to test
if __name__ == "__main__":
    target_url = "https://www.python.org"
    get_favicons(target_url)
```

**الناتج المتوقع (مقتطع للاختصار):**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

إذا كان الموقع يوفر فقط PNG أو Apple touch icons، سيعرض السكربت تلك العناوين بدلاً من ذلك، موضحًا لك بالضبط **كيف تحصل على أيقونة الموقع** في كل سيناريو.

## أسئلة شائعة وحالات خاصة  

### ماذا لو استخدم الموقع وسم `<meta>` بدلاً من `<link>`؟

بعض الصفحات القديمة تدمج عنوان الأيقونة في وسم `<meta name="msapplication‑TileImage">`. يمكنك توسيع `find_icon_links` للبحث أيضًا عن تلك الوسوم meta ومعالجتها بنفس الطريقة.

### كيف أتعامل مع الروابط النسبية التي تبدأ بـ `//`؟

`urljoin` يحل تلقائيًا الروابط النسبية للبرتوكول (`//example.com/favicon.ico`) بناءً على مخطط URL الأساسي، لذا لا تحتاج إلى منطق إضافي.

### هل يمكنني استرجاع أحجام متعددة (مثلاً 32×32، 180×180) تلقائيًا؟

نعم—فقط احذف خطوة `filter_ico_urls`. سيعيد السكربت كل عنوان أيقونة يكتشفه، بما في ذلك PNG بأحجام مختلفة. يمكنك بعد ذلك الفرز أو الاختيار بناءً على نمط اسم الملف.

### هل يعمل هذا على المواقع التي تحظر الروبوتات؟

إذا أعاد الموقع رمز 403 أو يتطلب User‑Agent مخصص، عدل استدعاء `requests.get` كالتالي:

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

هذا التعديل الصغير غالبًا ما يحل مشكلة “كيف تحصل على أيقونة الموقع” على النطاقات الأكثر صرامة.

## نظرة بصرية  

![مخطط يوضح تدفق عملية الحصول على أيقونة الموقع من موقع ويب – تحميل HTML، تحليل وسوم الرابط، استخراج href، تنزيل اختياري](how-to-get-favicon-diagram.png "مخطط تدفق الحصول على أيقونة الموقع")

*نص alt للصورة يحتوي على الكلمة المفتاحية الرئيسية، مما يلبي متطلبات SEO للصور.*

## الخلاصة  

لقد استعرضنا **كيف تحصل على أيقونة الموقع** خطوة بخطوة: تحميل HTML من URL،

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية حفظ HTML في C# – دليل كامل باستخدام معالج موارد مخصص](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [كيفية تحرير HTML باستخدام Aspose.HTML للـ Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [كيفية تحويل HTML إلى PDF باستخدام Java – باستخدام Aspose.HTML للـ Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}