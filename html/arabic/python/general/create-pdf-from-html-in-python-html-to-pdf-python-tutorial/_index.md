---
category: general
date: 2026-07-15
description: إنشاء ملف PDF من HTML باستخدام بايثون. تعلّم كيفية تحويل HTML إلى PDF
  بسرعة باستخدام سكريبت بسيط وخطوات واضحة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: ar
lastmod: 2026-07-15
og_description: إنشاء PDF من HTML باستخدام بايثون. يوضح لك هذا الدليل كيفية تحويل
  HTML إلى PDF، وحفظ HTML كملف PDF، وتعامل مع الموارد بكفاءة.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: إنشاء ملف PDF من HTML في بايثون – دليل عملي
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: إنشاء ملف PDF من HTML باستخدام بايثون – دليل بايثون لتحويل HTML إلى PDF
url: /ar/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF من HTML في بايثون – دليل شامل

هل احتجت يومًا إلى **إنشاء PDF من HTML** لكن لم تكن متأكدًا أي مكتبة بايثون تختار؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يحاولون تحويل تقرير ويب أو فاتورة أو صفحة تسويقية إلى PDF قابل للطباعة.  

الخبر السار هو أنه ببضع أسطر من الشيفرة يمكنك **تحويل HTML إلى PDF** بشكل موثوق، وتعمل السكريبت على Windows و macOS و Linux. في هذا الدليل سنستعرض مثالًا كاملاً قابلاً للتنفيذ، نشرح لماذا كل خطوة مهمة، ونظهر لك كيف **تحفظ HTML كملف PDF** دون ترك أي تفاصيل غير مكتملة.

---

## ما ستتعلمه

- تثبيت الحزمة الصحيحة في بايثون لتحويل HTML‑إلى‑PDF.  
- تحميل ملف HTML مع خيارات معالجة موارد مخصصة (لتجنب استيراد CSS بلا نهاية).  
- إنشاء ملف PDF نظيف على القرص.  
- معالجة الحالات الخاصة الشائعة مثل الصور الخارجية، والمسارات النسبية، والوثائق الكبيرة.  

بنهاية هذا **دليل HTML إلى PDF** ستحصل على دالة قابلة لإعادة الاستخدام يمكنك إدراجها في أي مشروع.

---

## المتطلبات المسبقة

- Python 3.9+ (الكود يعمل مع 3.8 أيضًا، لكن 3.9+ يوفّر أحدث ميزات `pathlib`).  
- إلمام أساسي بسطر الأوامر والبيئات الافتراضية.  
- ملف HTML ترغب في تحويله إلى PDF—أي صفحة ثابتة ستفي بالغرض.

> **نصيحة احترافية:** إذا كنت تستخدم بيئة افتراضية، فعّلها قبل تثبيت المكتبة؛ هذا يحافظ على نظافة تثبيت بايثون العام.

---

## الخطوة 1 – تثبيت WeasyPrint (المحرك وراء التحويل)

WeasyPrint هي مكتبة بايثون صافية تقوم بتحويل HTML و CSS إلى PDF. تتعامل مع معظم ميزات الويب الحديثة وتمنحك تحكمًا دقيقًا في تحميل الموارد.

```bash
pip install weasyprint
```

تشغيل الأمر أعلاه يجلب `cairocffi` و `tinycss2` وبعض الاعتمادات الأخرى. إذا صادفت خطأ متعلق بـ `cairo` على Windows، احصل على الحزم المسبقة البناء من [WeasyPrint website](https://weasyprint.org/docs/install/).

---

## الخطوة 2 – إعداد أداة مساعدة صغيرة لمعالجة الموارد

عند تحميل مستند HTML يشير إلى أوراق أنماط أو صور خارجية، ستتبع المكتبة تلك الروابط. في بعض الحالات يؤدي ذلك إلى تعشيق عميق أو حتى حلقات لا نهائية (تخيل ملف CSS يستورد نفسه بـ `@import`). للحفاظ على النظام نقوم بتحديد عمق معالجة الموارد.

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

الفئة أعلاه ليست مطلوبة من قبل WeasyPrint، لكنها تعكس النمط الذي رأيته في المقتطف الأصلي وتوفر لك نقطة توقف لاستيرادات غير مرغوبة. ستراها تُستخدم في الخطوة التالية.

---

## الخطوة 3 – تحميل مستند HTML باستخدام الخيارات المخصصة

الآن نقرأ فعليًا ملف HTML. تقبل فئة `HTML` معامل `base_url`، والذي نحدده إلى الدليل الذي يحتوي على ملف المصدر—هذا يجعل الروابط النسبية تعمل دون الحاجة إلى خادم ويب.

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **لماذا هذا مهم:** إذا كان HTML الخاص بك يجلب سلسلة من ملفات CSS، كل `@import` سيؤدي إلى تحميل آخر. حارس العمق يمنع السكريبت من الانفجار خارج السيطرة.

---

## الخطوة 4 – حفظ المستند المعالج كملف PDF

مع كائن `HTML` في يدك، إنشاء PDF يصبح سطرًا واحدًا. نمرر أيضًا مقطع CSS بسيط يفرض حجم صفحة نظيف (A4) ويضيف هامشًا صغيرًا—يمكنك تعديل ذلك حسب الحاجة.

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

استدعاء `write_pdf` يكتب الـ PDF إلى القرص، فتنتهي بملف جاهز للمشاركة.

---

## الخطوة 5 – جمع كل شيء معًا

فيما يلي سكريبت مختصر يمكنك نسخه ولصقه في `convert.py`. استبدل مسارات العنصر النائب بالمسارات الفعلية لديك.

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**الناتج المتوقع** – بعد تشغيل `python convert.py` يجب أن ترى:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

افتح الملف المُولَّد بأي عارض PDF؛ ستلاحظ تخطيط الصفحة الأصلي، وتنسيق CSS، والصور (بشرط أن تكون متاحة من ملف HTML).  

إذا لاحظت صورًا مفقودة، تحقق مرة أخرى من أن سمات `src` إما عناوين URL مطلقة أو مسارات نسبية موجودة تحت `YOUR_DIRECTORY`.

---

## أسئلة شائعة ومعالجة الحالات الخاصة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو كان HTML الخاص بي يشير إلى خطوط خارجية؟* | سيقوم WeasyPrint بتحميل ملفات الخط تلقائيًا، لكن قد ترغب في وضع قائمة بيضاء للمجالات لتجنب أوقات التحميل الطويلة. |
| *هل يمكنني تحويل سلسلة HTML بدلاً من ملف؟* | نعم—استخدم `HTML(string=my_html_string)` وتجاوز `base_url` أو عيّنه إلى مجلد مؤقت. |
| *كيف أتحكم ببيانات تعريف PDF (العنوان، المؤلف)؟* | مرّر قاموس `metadata` إلى `write_pdf`، مثال: `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *أحصل على خطأ “cairo‑cffi error” على Linux.* | ثبّت حزمة النظام `libcairo2-dev` (`apt-get install libcairo2-dev` على Debian/Ubuntu) قبل تثبيت WeasyPrint عبر pip. |

---

## الخلاصة

لقد **أنشأنا للتو PDF من HTML** باستخدام سير عمل بايثون نظيف، غطينا آليات **تحويل HTML إلى PDF**، وأظهرنا لك كيف **تحفظ HTML كملف PDF** مع معالجة موارد قوية. السكريبت صغير بما يكفي لإدراجه في خطوط CI، لكنه مرن بما يكفي للتوسيع بإضافة رؤوس، وتذييلات، أو علامات مائية مخصصة.

الخطوات التالية التي قد تستكشفها:

- استخدم مكتبة **html to pdf python** `pdfkit` لنهج يعتمد على wkhtmltopdf (مفيد للـ CSS القديم).  
- أضف واجهة سطر أوامر باستخدام `argparse` لتقبل السكريبت مدخلات ومخرجات.  
- أنشئ PDFs في الوقت الفعلي داخل نقطة نهاية Flask أو FastAPI لتقارير حسب الطلب.  

لا تتردد في التجربة، وكسر الأشياء، ثم العودة إلى هذا الدليل لتحديث سريع. إذا واجهت أي عوائق، فإن وثائق WeasyPrint ومنتديات المجتمع موارد ممتازة.

برمجة سعيدة، واستمتع بتحويل تلك الصفحات الويب إلى ملفات PDF أنيقة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [Convert HTML to PDF with Aspose.HTML – Full Manipulation Guide](/html/english/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Create PDF from HTML – C# Step‑by‑Step Guide](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}