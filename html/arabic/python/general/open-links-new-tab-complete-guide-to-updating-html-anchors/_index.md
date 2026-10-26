---
category: general
date: 2026-07-05
description: فتح الروابط في تبويب جديد باستخدام بايثون – تعلم كيفية إضافة target="_blank"،
  تغيير هدف الرابط، استخدام محدد يحتوي على السمة، وحفظ الـ HTML المعدل بسهولة.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: ar
og_description: افتح الروابط في علامة تبويب جديدة بسرعة. يوضح هذا الدرس كيفية إضافة
  target="_blank"، وتغيير هدف الرابط، وحفظ ملف HTML المعدل باستخدام بايثون.
og_title: فتح الروابط في تبويب جديد – دليل تحديث HTML خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: فتح الروابط في علامة تبويب جديدة – دليل كامل لتحديث الروابط في HTML
url: /ar/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# فتح الروابط في علامة تبويب جديدة – دليل كامل لتحديث روابط HTML

هل احتجت يومًا إلى **open links new tab** على صفحة HTML ثابتة لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك. يواجه العديد من المطورين هذه المشكلة عند تنظيف المواقع القديمة أو إضافة تحسينات الوصول. في هذا الدرس سنستعرض حلًا عمليًا يقوم بـ **adds target blank**، **changes link target**، ويحفظ **saves modified html** بأمان — كل ذلك ببضع أسطر من Python.

سنتناول أيضًا كيفية استخدام **attribute contains selector** حتى لا تتعامل إلا مع الروابط التي تهمك حقًا (على سبيل المثال، كل رابط يشير إلى *example.com*). في النهاية، ستحصل على سكريبت قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع، بغض النظر عن حجمه.

## ما ستتعلمه

- تحميل ملف HTML إلى كائن مستند قابل للتعديل.  
- اختيار عناصر `<a>` التي يحتوي سمة `href` الخاصة بها على جزء نصي محدد.  
- **Add target blank** وتعيين سمة `rel="noopener"` لتحسين الأمان.  
- **Save modified html** مرة أخرى إلى القرص دون فقدان التنسيق.  

لا توجد تبعيات خارجية سوى المكتبة القياسية و **beautifulsoup4** (تثبيت صغير). إذا كنت تستخدم محللًا مختلفًا بالفعل، فإن المفاهيم تنطبق مباشرة.

---

## المتطلبات المسبقة

- Python 3.8+ مثبت على جهازك.  
- إلمام أساسي بـ HTML و Python.  
- `beautifulsoup4` package (`pip install beautifulsoup4`).  

هذا كل شيء — لا حاجة لأطر عمل ضخمة.

---

## الخطوة 1: تحميل مستند HTML

أولاً وقبل كل شيء: نحتاج إلى قراءة ملف المصدر وتسليمه إلى BeautifulSoup. فكر في ذلك كفتح لوحة فارغة يمكنك رسم سمات جديدة عليها.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **لماذا هذا مهم:** استخدام `Path` يجعل الكود مستقلًا عن نظام التشغيل، و`html.parser` مدمج، لذا لا تحتاج إلى محللات إضافية للمهام البسيطة.

---

## الخطوة 2: استخدام **attribute contains selector** للعثور على الروابط الصحيحة

نريد فقط تعديل الروابط التي تشير إلى *example.com*. محدد CSS `a[href*='example.com']` يفعل ذلك بالضبط — `*=` يعني “contains”. طريقة `select` في BeautifulSoup تفهم هذا الصياغ.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **نصيحة احترافية:** إذا كنت بحاجة إلى مطابقة غير حساسة لحالة الأحرف، انتقل إلى حلقة صغيرة تتحقق من `if 'example.com' in a.get('href', '').lower()`.

الآن يحتوي `anchor_elements` على كل رابط نهتم به، جاهز للتحويل التالي.

---

## الخطوة 3: تغيير هدف الرابط – إضافة target blank وتأمين الرابط

فتح رابط في علامة تبويب جديدة بسيط مثل تعيين `target="_blank"`. ومع ذلك، توصي المتصفحات الحديثة أيضًا بإضافة `rel="noopener"` (أو `noreferrer`) لمنع الصفحة المفتوحة حديثًا من الوصول إلى النافذة الأصلية عبر `window.opener`. هذه التعديلة الأمنية الصغيرة يمكن أن توقف هجمات التصيد.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **لماذا نستخدم تعيين القاموس المباشر:** فهو ينشئ السمة تلقائيًا إذا كانت مفقودة، ويستبدلها إذا كانت موجودة بالفعل — مثالي لعملية **change link target**.

---

## الخطوة 4: حفظ HTML المعدل مرة أخرى إلى القرص

الخطوة الأخيرة هي كتابة العلامات المحدثة إلى ملف جديد. الحفاظ على الأصل دون تعديل يتيح لك الرجوع إذا حدث خطأ.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **ما تقوم به `prettify()`:** تقوم بتنسيق HTML مع مسافات بادئة جميلة، مما يجعل الملف المحفوظ أسهل للقراءة والمقارنة لاحقًا. إذا كنت تفضل المسافات الأصلية، استبدل `prettify()` بـ `str(soup)`.

---

## السكريبت الكامل – حل بنقرة واحدة

فيما يلي السكريبت الكامل الجاهز للتنفيذ. احفظه باسم `update_links.py` وشغّله باستخدام `python update_links.py` من الطرفية.

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### النتيجة المتوقعة

افترض أن `links.html` يحتوي أصلاً على:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

بعد تشغيل السكريبت، سيظهر `links-updated.html` كالتالي:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

فقط الرابط إلى *example.com* حصل على سمات **add target blank**، مما يثبت أن **attribute contains selector** عمل كما هو مقصود.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو كان للربط سمة `rel` موجودة بالفعل؟

تقوم حلقتنا بالكتابة فوقها بـ "noopener". إذا كنت بحاجة إلى الحفاظ على القيم الموجودة (مثل "nofollow"), فقم بالدمج بدلاً من ذلك:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### كيف تتعامل مع عدة نطاقات؟

فقط قم بتوسيع قائمة المحددات:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### هل `prettify()` يغيّر بنية HTML الأصلية؟

إنه يعيد تنسيق المسافات لكنه لا يغيّر ترتيب الوسوم أو قيم السمات. إذا كان عليك الحفاظ على المسافات الأصلية تمامًا، استبدل `prettify()` بـ `str(soup)` كما ذكرنا سابقًا.

---

## نصائح احترافية للسكريبتات الجاهزة للإنتاج

- **Backup before overwriting:** أضف خطوة نسخ (`shutil.copy`) للحفاظ على الملف الأصلي آمنًا.  
- **Logging instead of print:** استخدم وحدة `logging` للمشاريع القابلة للتوسع.  
- **Batch processing:** قم بالتكرار على دليل باستخدام `Path.rglob("*.html")` لتحديث العديد من الملفات في تشغيل واحد.  

هذه التعديلات تحول سكريبت **open links new tab** البسيط إلى أداة قوية لأي سير عمل صيانة ويب.

---

## الخلاصة

أصبح لديك الآن طريقة قوية وقابلة لإعادة الاستخدام لـ **open links new tab** عبر أي مجموعة من ملفات HTML الثابتة. من خلال الاستفادة من **attribute contains selector**، يمكنك **change link target** بدقة حيث تحتاج، **add target blank**، و **save modified html** دون فقدان التنسيق.

جرّبه على صفحة اختبار، ثم قم بتوسيع النطاق إلى موقعك بالكامل. هل تحتاج إلى تعديل المحدد للملفات PDF أو نطاقات أخرى؟ فقط عدل سلسلة CSS — كل شيء آخر يبقى كما هو.

لا تتردد في ترك تعليق إذا واجهت أي مشاكل، أو مشاركة كيف قمت بتوسيع السكريبت لمشاريعك الخاصة. برمجة سعيدة، ولتفتح جميع روابطك تمامًا حيث تريد!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تعديل HTML باستخدام Aspose.HTML للـ Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [كيفية إضافة CSS – CSS مضمن إلى مستندات HTML في Aspose.HTML للـ Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}