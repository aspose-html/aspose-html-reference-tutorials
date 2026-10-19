---
category: general
date: 2026-07-27
description: كيفية استخدام SaveOptions في Aspose.HTML (Python) لتحويل صفحة HTML كبيرة
  وتطبيق معالجة الموارد بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: ar
lastmod: 2026-07-27
og_description: كيفية استخدام SaveOptions في Aspose.HTML (Python) يتيح لك تحويل صفحة
  HTML كبيرة مع تطبيق معالجة الموارد للحصول على نتائج نظيفة وسريعة.
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: كيفية استخدام SaveOptions في Aspose.HTML – دليل بايثون
schemas:
- author: Aspose
  dateModified: '2026-07-27'
  description: How to use SaveOptions in Aspose.HTML (Python) to convert large HTML
    page and apply resource handling efficiently.
  headline: How to Use SaveOptions in Aspose.HTML (Python)
  type: TechArticle
- questions:
  - answer: Aspose.HTML follows redirects but won’t send credentials automatically.
      You can pre‑download those assets or use a custom `WebRequest` handler (beyond
      this guide’s scope).
    question: What if the page references resources over HTTPS that require authentication?
  - answer: Yes—set `resource_options.max_handling_depth = 0`. This skips external
      files but leaves any `<style>` blocks intact.
    question: Can I preserve inline CSS while stripping external files?
  - answer: After saving, you can run a secondary pass with Pillow to downscale images,
      or let Aspose.HTML’s built‑in image compression options handle it (use `save_options.image_quality`).
    question: What about very large images that still bloat the output?
  - answer: The limit is global across all resource types (images, scripts, styles).
      If you need granular control, you’d have to filter resources manually after
      loading the document.
    question: Is the depth limit applied per‑resource type?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- HTML processing
title: كيفية استخدام SaveOptions في Aspose.HTML (Python)
url: /ar/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام SaveOptions في Aspose.HTML (Python)

كيفية استخدام SaveOptions في Aspose.HTML لـ Python هي سؤال يطرحه العديد من المطورين عند التعامل مع ملفات HTML الضخمة. إذا كنت بحاجة إلى **تحويل صفحة HTML كبيرة** مع الحفاظ على سيطرة دقيقة على **معالجة الموارد**، فأنت في المكان الصحيح.  

في هذا الدرس سنستعرض سيناريو واقعي: أخذ صفحة HTML ضخمة، تحديد مدى عمق سحب الموارد المتداخلة، وأخيرًا حفظ (أو تحويل) النتيجة بتحكم واضح. لا مراجع غامضة، فقط مثال كامل قابل للتنفيذ يمكنك نسخه ولصقه في مشروعك اليوم.

> **نصيحة احترافية:** `SaveOptions` في Aspose.HTML لا يعمل فقط لحفظ الملف كـ HTML بل أيضًا للتحويل إلى PDF أو PNG أو حتى DOCX. النمط نفسه الذي نغطيه أدناه ينطبق على جميع تلك الصيغ.

---

## ما ستحتاجه

- **Python 3.8+** (الكود يستخدم تلميحات النوع لكنه يعمل على أي نسخة حديثة)  
- **Aspose.HTML for Python via .NET** – تثبيت عبر `pip install aspose-html`  
- ملف **HTML كبير** تريد تقليصه أو تحويله (المثال يستخدم `big_page.html`)  
- مساحة قرص معتدلة لملف الإخراج  

هذا كل شيء—بدون مكتبات إضافية، بدون أدوات بناء ثقيلة.

---

## كيفية استخدام SaveOptions مع خيارات معالجة الموارد

هذا هو جوهر الموضوع. سننشئ كائن `SaveOptions`، نرفق به كائن `ResourceHandlingOptions` يحدد لــ Aspose.HTML مدى العمق الذي يجب أن يتبع فيه الموارد المرتبطة، ثم نمرر كل ذلك إلى طريقة `save` الخاصة بالمستند.

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Load the source HTML document
input_path = "YOUR_DIRECTORY/big_page.html"
doc = HTMLDocument(input_path)

# Define how deep nested resources should be processed (limit to 3 levels)
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # <-- controls depth of resource fetching

# Attach the resource handling configuration to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# Save the processed document (or convert to another format if desired)
output_path = "YOUR_DIRECTORY/big_page_processed.html"
doc.save(output_path, save_options)
```

**لماذا هذا يعمل:**  
- `HTMLDocument` يحمل الملف الأصلي، ويحلل كل `<img>` و `<link>` و `<script>` وغيرها.  
- `ResourceHandlingOptions.max_handling_depth` يخبر المحرك بالتوقف عن متابعة الموارد بعد ثلاثة مستويات من التداخل—مثالي لتجنب الحلقات اللانهائية في الصفحات التي تدمج صفحات أخرى.  
- `SaveOptions` هو الوعاء الذي يحمل كلًا من صيغة الإخراج (HTML افتراضيًا) وقواعد معالجة الموارد.  
- أخيرًا، `doc.save` يكتب الملف الجديد، مطبقًا القواعد التي حددناها.

عند تشغيل السكريبت، ستظهر لك ملف جديد باسم `big_page_processed.html`. افتحه في المتصفح؛ ستلاحظ أن جميع الصور، الأنماط، والسكريبتات حتى ثلاثة مستويات من العمق لا تزال موجودة، بينما تم حذف الإشارات الأعمق. هذا يقلل حجم الملف بشكل كبير دون كسر تخطيط الصفحة—بالضبط ما تحتاجه عندما **تحول صفحة HTML كبيرة** للاستخدام دون اتصال أو لإرسالها عبر البريد الإلكتروني.

---

## تحويل صفحة HTML الكبيرة بكفاءة

إذا كان هدفك هو *تحويل صفحة HTML كبيرة* إلى نسخة أصغر، فإن المقتطف أعلاه يقوم بمعظم العمل الشاق. ومع ذلك، قد ترغب في تغيير صيغة الإخراج تمامًا. تجعلك Aspose.HTML تقوم بذلك بسطر واحد:

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

فقط استبدل الخاصية `format` بـ `"PNG"` أو `"JPEG"` أو `"DOCX"` وستحصل على خط أنابيب تحويل كامل. تبقى قواعد **معالجة الموارد** نفسها، لذا فإن ملف PDF الناتج لن يضم كل ملف CSS خارجي من الموقع الأصلي—فقط تلك التي تقع ضمن عمق الثلاث مستويات التي حددتها.

---

## تطبيق معالجة الموارد على الموارد المتداخلة

لنتعمق قليلًا في **معالجة الموارد** بفعالية. افترض أن ملف HTML يحتوي على ورقة أنماط تستورد أوراق أنماط أخرى، وكل واحدة منها تجلب صورًا. بدون حد للعمق، قد يتبع Aspose.HTML السلسلة إلى ما لا نهاية، مما يثقل الذاكرة واستهلاك المعالج.

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **العمق 0** – لا يتم جلب أي موارد خارجية؛ تحصل على هيكل HTML بسيط جدًا.  
- **العمق 1** – تُضمَّن فقط الموارد من المستوى الأول (علامات `<img>` المباشرة، ملفات CSS الفورية).  
- **العمق 2+** – يُحترم التداخل الأعمق، وهو مفيد للمواقع المعقدة التي تعتمد الأنماط على أنماط أخرى.

اختر العمق الذي يتناسب مع سيناريو **تحويل صفحة HTML كبيرة** الخاص بك. بالنسبة للنشرات البريدية، غالبًا ما يكون العمق 1 كافيًا. بالنسبة للأرشفة المحلية، يُعطي العمق 3 (كما في المثال الرئيسي) توازنًا جيدًا.

---

## مثال عملي كامل – من البداية إلى النهاية

فيما يلي سكريبت مستقل يمكنك وضعه في ملف باسم `process_html.py`. يتضمن معالجة الأخطاء، التسجيل، ومساعدًا صغيرًا يطبع لك نسبة تقليل الحجم التي حققتها.

```python
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

def process_html(
    src_path: str,
    dst_path: str,
    depth: int = 3,
    fmt: str = "HTML"
) -> None:
    """
    Loads an HTML file, applies resource handling, and saves it in the requested format.
    Returns nothing; prints size statistics for quick verification.
    """
    if not os.path.isfile(src_path):
        raise FileNotFoundError(f"Source file not found: {src_path}")

    # Load document
    doc = HTMLDocument(src_path)

    # Set up resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = depth

    # Configure save options (including format)
    save_opts = SaveOptions()
    save_opts.resource_handling_options = res_opts
    save_opts.format = fmt.upper()   # Aspose expects upper‑case format strings

    # Perform save / conversion
    doc.save(dst_path, save_opts)

    # Report size change
    original = os.path.getsize(src_path)
    final = os.path.getsize(dst_path)
    reduction = (original - final) / original * 100
    print(f"Saved {fmt.lower()} to '{dst_path}'. Size reduced by {reduction:.2f}%.")

# -------------------------------------------------------------------------
# Example usage
if __name__ == "__main__":
    input_file = "YOUR_DIRECTORY/big_page.html"
    output_file = "YOUR_DIRECTORY/big_page_processed.html"

    process_html(
        src_path=input_file,
        dst_path=output_file,
        depth=3,          # apply resource handling up to three levels
        fmt="HTML"       # change to "PDF" or "PNG" to convert format
    )
```

**المخرجات المتوقعة (وحدة التحكم):**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

افتح الملف المعالج؛ ستلاحظ صفحة أخف وزنًا لا تزال تشبه الأصل. إذا غيرت `fmt` إلى `"PDF"`، سيظهر في وحدة التحكم حجم ملف PDF ويمكنك فتحه بأي عارض PDF.

---

## أسئلة شائعة وحالات خاصة

- **ماذا لو كانت الصفحة تشير إلى موارد عبر HTTPS تتطلب مصادقة؟**  
  Aspose.HTML يتبع عمليات إعادة التوجيه لكنه لا يرسل بيانات الاعتماد تلقائيًا. يمكنك تنزيل تلك الأصول مسبقًا أو استخدام معالج `WebRequest` مخصص (خارج نطاق هذا الدليل).

- **هل يمكنني الحفاظ على CSS المضمن بينما أحذف الملفات الخارجية؟**  
  نعم—اضبط `resource_options.max_handling_depth = 0`. سيتخطى ذلك الملفات الخارجية لكنه يترك أي كتل `<style>` سليمة.

- **ماذا عن الصور الكبيرة التي لا تزال ترفع حجم الإخراج؟**  
  بعد الحفظ، يمكنك تشغيل خطوة ثانية باستخدام Pillow لتقليل أبعاد الصور، أو السماح لخيارات ضغط الصور المدمجة في Aspose.HTML (استخدم `save_options.image_quality`).

- **هل يُطبق حد العمق على كل نوع من الموارد بشكل منفصل؟**  
  الحد عالمي عبر جميع أنواع الموارد (الصور، السكريبتات، الأنماط). إذا احتجت تحكمًا دقيقًا، سيتعين عليك تصفية الموارد يدويًا بعد تحميل المستند.

---

## الخلاصة

أصبح لديك الآن فهم قوي **لكيفية استخدام SaveOptions** في Aspose.HTML

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تحويل HTML إلى PDF باستخدام Java – باستخدام Aspose.HTML لـ Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [كيفية تحويل HTML إلى MHTML باستخدام Aspose.HTML لـ Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [كيفية استخدام Aspose لتصوير HTML إلى PNG – دليل خطوة بخطوة](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}