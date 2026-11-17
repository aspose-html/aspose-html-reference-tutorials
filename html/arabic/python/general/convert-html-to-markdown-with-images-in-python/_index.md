---
category: general
date: 2026-11-17
description: تحويل HTML إلى markdown مع الصور في بايثون – تعلّم كيفية تحويل HTML بسرعة
  مع تصدير الصور دون تعديل.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to convert html
- export html with images
- markdown conversion with images
language: ar
lastmod: 2026-11-17
og_description: تحويل HTML إلى ماركداون مع الصور في بايثون. يوضح هذا الدرس كيفية تحويل
  HTML مع تصدير الصور، مما يمنحك حلاً كاملاً جاهزًا للتنفيذ.
og_image_alt: Diagram showing convert html to markdown workflow with image extraction
og_title: تحويل HTML إلى ماركداون مع الصور في بايثون – دليل سريع
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Convert HTML to markdown with images in Python – learn how to convert
    HTML quickly while exporting images intact.
  headline: Convert HTML to markdown with images in Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- Image extraction
title: تحويل HTML إلى ماركداون مع الصور في بايثون
url: /ar/python/general/convert-html-to-markdown-with-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل HTML إلى markdown مع الصور في Python

إذا كنت بحاجة إلى **تحويل HTML إلى markdown** مع الحفاظ على الصور كملفات منفصلة، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. ستحصل على مثال كامل قابل للتنفيذ يتعامل مع الموارد الخارجية، بحيث يشير ناتج markdown إلى الصور الأصلية بشكل صحيح.

تصدير HTML مع الصور غالبًا ما يُعرّق المحولات البسيطة لأنها إما تُهمل الصور أو تُدمجها كسلاسل base64. من خلال ضبط خيارات معالجة الموارد، تحتفظ بالملفات الأصلية للصور وتنتج markdown نظيف يمكن التحكم فيه عبر نظام الإصدارات أو تحريره لاحقًا.

في هذا الدرس ستقوم بـ:

* تحميل مستند HTML من القرص.  
* ضبط المحول لت **تصدير HTML مع الصور** كملفات منفصلة.  
* حفظ النتيجة كـ markdown باستخدام خيارات **تحويل markdown مع الصور**.  

المتطلب الوحيد هو وجود نسخة حديثة من مكتبة Aspose.HTML للـ Python (أو أي API متوافق يوفر `HTMLDocument`، `ResourceHandlingOptions`، `MarkdownSaveOptions`، و`Converter`). كما تحتاج إلى Python 3.8+ وإذن كتابة على مجلد الإخراج.

---

## المتطلبات المسبقة والتثبيت

1. تثبيت حزمة Aspose.HTML:

   ```bash
   pip install aspose-html
   ```

2. التحقق من التثبيت:

   ```python
   import aspose.html as ah
   print(ah.__version__)   # should print the installed version, e.g., 22.9
   ```

> **نصيحة احترافية:** استخدم بيئة افتراضية لتجنب تعارض الإصدارات مع المشاريع الأخرى.

---

## الخطوة 1: تحميل مستند HTML المصدر

الخطوة الأولى هي إنشاء كائن `HTMLDocument` يمثل الملف المصدر. يقوم هذا الكائن بتحليل العلامات وبناء شجرة DOM يمكن للمحول استعراضها.

```python
from aspose.html import HTMLDocument

# Load the HTML file you want to convert
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*لماذا هذا مهم* – تحميل المستند يمنح المكتبة سيطرة كاملة على العلامات، مما يسمح لها بحل عناوين URL النسبية وتطبيق معالجة الموارد لاحقًا.

---

## الخطوة 2: ضبط معالجة الموارد الخارجية

عند **تصدير HTML مع الصور**، عادةً ما تريد حفظ الصور بجوار ملف markdown بدلاً من دمجها. تسمح لك فئة `ResourceHandlingOptions` بتحديد هذا السلوك.

```python
from aspose.html import ResourceHandlingOptions

resource_options = ResourceHandlingOptions()
resource_options.save_external_resources = True   # keep images as separate files
```

تعيين `save_external_resources` إلى `True` يوجه المحول لنسخ كل مورد خارجي (صور، CSS، خطوط) إلى مجلد بجانب ملف markdown الناتج. سيحتوي ملف markdown على روابط نسبية تشير إلى تلك النسخ.

---

## الخطوة 3: إرفاق تكوين معالجة الموارد إلى خيارات markdown

تتحكم `MarkdownSaveOptions` في طريقة التحويل إلى markdown. من خلال تعيين الخاصية `resource_handling_options`، تُفعِّل ميزة **تحويل markdown مع الصور**.

```python
from aspose.html import MarkdownSaveOptions

markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options
```

إذا تخطيت هذه الخطوة، سيقوم المحول بإزالة مراجع الصور أو دمجها كـ data URIs، مما يُفقد هدف تصدير الصور.

---

## الخطوة 4: تنفيذ التحويل

أخيرًا، استدعِ `Converter.convert` مع المستند المصدر، مسار الهدف، والخيارات التي أعددتها.

```python
from aspose.html import Converter

output_path = "YOUR_DIRECTORY/sample.md"
Converter.convert(html_doc, output_path, markdown_options)
```

بعد اكتمال الاستدعاء، ستجد:

* `sample.md` – نسخة markdown من HTML الأصلي.  
* مجلد فرعي يُسمى `sample_files` (أو ما شابه) يحتوي على كل صورة تم الإشارة إليها في HTML.

---

## البرنامج النصي الكامل

دمج جميع الأجزاء معًا يمنحك سكريبتًا واحدًا يمكنك تشغيله من سطر الأوامر:

```python
# convert_html_to_markdown.py
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, MarkdownSaveOptions, Converter

def convert_html_to_markdown(html_file: str, markdown_file: str):
    """
    Convert an HTML file to markdown while exporting images as separate files.
    """
    # 1. Load the HTML document
    html_doc = HTMLDocument(html_file)

    # 2. Set up resource handling to keep images external
    res_opts = ResourceHandlingOptions()
    res_opts.save_external_resources = True

    # 3. Attach resource handling to markdown options
    md_opts = MarkdownSaveOptions()
    md_opts.resource_handling_options = res_opts

    # 4. Convert and save
    Converter.convert(html_doc, markdown_file, md_opts)
    print(f"Conversion complete: {markdown_file}")

if __name__ == "__main__":
    # Adjust these paths to your environment
    src_html = os.path.abspath("YOUR_DIRECTORY/sample.html")
    dst_md   = os.path.abspath("YOUR_DIRECTORY/sample.md")

    convert_html_to_markdown(src_html, dst_md)
```

**الناتج المتوقع**

```
Conversion complete: /absolute/path/YOUR_DIRECTORY/sample.md
```

بعد التنفيذ، افتح `sample.md` في أي محرر markdown. ستظهر روابط الصور كالتالي:

```markdown
![Alt text](sample_files/image1.png)
```

الصور نفسها موجودة في مجلد `sample_files`، جاهزة للتحكم في الإصدارات أو المعالجة الإضافية.

---

## معالجة الحالات الشائعة

| الحالة | النهج الموصى به |
|--------|-----------------|
| **ملفات الصور المفقودة** | يسجل المحول تحذيرًا ويترك رابطًا مكسورًا. تأكد من أن جميع سمات `<img src>` تشير إلى موارد يمكن الوصول إليها قبل التحويل. |
| **روابط URL نسبية تشير إلى خارج مجلد المشروع** | استخدم `ResourceHandlingOptions.base_url` لتوفير عنوان URL أساسي حتى يتمكن المحول من حل المسارات بشكل صحيح. |
| **ملفات HTML الكبيرة مع العديد من الصور** | عيّن `resource_options.max_resource_size` (إن كان متاحًا) لتحديد الحد الأقصى لحجم الموارد التي تُنسخ. |
| **صيغ صور غير PNG/JPEG** | تقوم المكتبة بنسخ الصيغة الأصلية تلقائيًا. تأكد من أن عارض markdown المستهدف يدعم الصيغة (مثل SVG). |
| **أخطاء صلاحية الكتابة** | شغّل السكريبت بالأذونات المناسبة أو اختر دليل إخراج لديك صلاحية كتابة فيه. |

---

## نصائح لتحويل markdown مع الصور بسلاسة

* حافظ على نظافة مجلد الإخراج: احذف دليل `*_files` قبل كل تشغيل إذا أردت مجموعة جديدة من الصور.  
* استخدم سمات `alt` ذات معنى في HTML الأصلي؛ فهي تتحول تلقائيًا إلى تعليقات صور markdown.  
* إذا كنت بحاجة إلى دمج الصور كـ base64 (لملف markdown موحد)، عيّن `resource_options.save_external_resources = False`. هذا عكس **تصدير HTML مع الصور**، لكنه مفيد للبريد الإلكتروني أو تضمين الوثائق.  
* عند تحويل مجموعة من الملفات، غلف السكريبت بحلقة وعدّل `resource_options.resource_folder` لتجنب تصادم الأسماء.

---

## الأسئلة المتكررة

**س: هل يعمل هذا مع أجزاء HTML تفتقر إلى غلاف `<html>` كامل؟**  
ج: نعم. يمكن لـ `HTMLDocument` تحليل الأجزاء؛ يتعامل المحول معها كـ

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to embed images in HTML to Markdown conversion using Python](/html/english/python/general/how-to-embed-images-in-html-to-markdown-conversion-using-pyt/)
- [Convert HTML to Markdown – Complete Guide with CSS & Images](/html/english/python/general/convert-html-to-markdown-complete-guide-with-css-images/)
- [Convert HTML to Markdown with Aspose – Complete Python Guide](/html/english/python/general/convert-html-to-markdown-with-aspose-complete-python-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}