---
date: 2026-05-30
description: تعلم كيفية تحويل EPUB إلى PDF في Java باستخدام Aspose.HTML مع ضبط حجم
  صفحة PDF مخصص وخيارات حفظ PDF أخرى.
keywords:
- custom pdf page size
- convert epub to pdf
- change pdf background color
- specify pdf page dimensions
- aspose.html java
linktitle: تحديد خيارات حفظ PDF لتحويل EPUB إلى PDF
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  headline: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  type: TechArticle
- description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  name: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  steps:
  - name: Open the EPUB File
    text: First, create a `FileInputStream` that points to your source `.epub`. Keeping
      the stream open until the conversion finishes prevents “blank page” errors.
  - name: Define PDF Save Options
    text: '`PdfSaveOptions` is Aspose.HTML''s configuration class that controls PDF
      output settings such as page size, background color, and margins. `Length.fromPixels`
      converts screen pixels to PDF points (1 point = 1/72 inch), allowing you to
      specify dimensions in familiar pixel units.'
  - name: Convert EPUB to PDF
    text: With the input stream and custom options ready, invoke the converter. The
      output PDF will be saved to the location you specify, preserving the exact page
      dimensions you defined. `PdfSaveOptions.setEnableParallelProcessing` is a method
      that enables parallel processing of pages during PDF conversion.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a commercial library, but you can obtain a free
      trial version from their [website](https://releases.aspose.com/).
    question: Is Aspose.HTML for Java a free library?
  - answer: Aspose.HTML for Java supports EPUB 2.0, EPUB 3.0, and EPUB 3.1, handling
      re‑flowable and fixed‑layout books with full CSS support.
    question: What EPUB formats are supported for conversion?
  - answer: Yes, you can customize the PDF output by adjusting the page setup, background
      color, compression level, and other settings in the `PdfSaveOptions`.
    question: Can I customize the PDF output further?
  - answer: The trial version may add a watermark to the first few pages and limits
      the maximum file size to 10 MB; purchase a license to remove these restrictions.
    question: Are there any limitations to the trial version of Aspose.HTML for Java?
  - answer: You can find answers to your questions and seek support on the [Aspose.HTML
      forum](https://forum.aspose.com/).
    question: Where can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: حجم صفحة PDF مخصص - تحديد خيارات حفظ PDF لتحويل EPUB إلى PDF
url: /ar/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حجم صفحة PDF مخصص: تحديد خيارات حفظ PDF لتحويل EPUB إلى PDF

## مقدمة

Aspose.HTML for Java يجعل من السهل **تحويل EPUB إلى PDF** ويمنحك تحكمًا كاملاً في الناتج، بما في ذلك ضبط **حجم صفحة PDF مخصص**. في هذا الدليل خطوة بخطوة سنستعرض كل ما تحتاجه—من إعداد بيئتك إلى تعديل `PdfSaveOptions` بحيث يتطابق PDF المُنشأ مع أبعاد الصفحة الدقيقة التي تحتاجها. سواء كنت تبني خط أنابيب نشر، أو منصة تعلم إلكتروني، أو فقط تحتاج إلى أتمتة تحويل المستندات، ستجد التقنيات هنا ذات قيمة.

## إجابات سريعة
- **ما هو الهدف الأساسي من هذا الدليل؟** تحويل ملف EPUB إلى PDF مع تطبيق حجم صفحة PDF مخصص.  
- **ما المكتبة المستخدمة؟** Aspose.HTML for Java.  
- **هل أحتاج إلى ترخيص؟** يتوفر نسخة تجريبية مجانية؛ يلزم ترخيص تجاري للإنتاج.  
- **هل يمكنني تغيير لون الخلفية؟** نعم، باستخدام `PdfSaveOptions`.  
- **هل يدعم Java 8+؟** بالطبع—أي بيئة تشغيل Java حديثة تعمل.

## ما هو حجم صفحة PDF مخصص؟

يسمح لك حجم صفحة PDF مخصص بتحديد العرض والارتفاع الدقيق لكل صفحة في PDF الناتج، بدلاً من الاعتماد على الأحجام القياسية مثل A4 أو Letter. يمكنك ضبط الأبعاد بالنقاط (1 نقطة = 1/72 بوصة) أو التحويل من البكسل، مما يمنحك تحكمًا مثاليًا بالبكسل في التخطيط النهائي. هذا مثالي للكتب الإلكترونية، والنشرات، أو أي تصميم يجب أن يتطابق مع تنسيق محدد مسبقًا دون معالجة يدوية لاحقة.

## لماذا تستخدم Aspose.HTML لتحويل EPUB إلى PDF؟

يقوم Aspose.HTML بتحويل EPUB إلى PDF في سطرين من الشيفرة مع الحفاظ على التخطيطات المعقدة، الخطوط المدمجة، والصور عالية الدقة. يدعم **أكثر من 50 تنسيقًا للمدخلات والمخرجات**، ويمكنه إنشاء ملفات PDF تصل إلى **2,000 صفحة** دون تحميل الملف بالكامل في الذاكرة، ويعمل على Windows وLinux وmacOS بنفس النتائج. كما توفر المكتبة خيارات حفظ PDF دقيقة، تتيح لك تعديل حجم الصفحة، لون الخلفية، الهوامش، وإعدادات الضغط—كل ذلك من Java.

## المتطلبات المسبقة
- **Java Development Environment:** JDK 8 أو أحدث مثبت ومُكوَّن.  
- **Aspose.HTML for Java:** تحميل أحدث JAR من [الموقع](https://releases.aspose.com/html/java/).  
- **EPUB File:** مستند `.epub` ترغب في تحويله.  

الآن بعد أن أصبح كل شيء جاهزًا، دعنا نغوص في خطوات التحويل الفعلية.

## كيفية تحويل EPUB إلى PDF بحجم صفحة مخصص؟

`FileInputStream` هي فئة Java تقرأ البايتات الخام من ملف.  
`PdfSaveOptions` هي فئة في Aspose.HTML تُكوّن إعدادات إخراج PDF مثل حجم الصفحة ولون الخلفية.  
حمّل ملف EPUB باستخدام `FileInputStream`، واضبط `PdfSaveOptions` لتحديد أبعاد الصفحة الدقيقة، ثم استدعِ المحول. يُجري سير العمل المكوّن من ثلاث خطوات التحويل في أقل من دقيقة لأحجام الكتب الإلكترونية النموذجية، ويتوسع للمجموعات الأكبر مع تغييرات قليلة في الشيفرة.

### الخطوة 1: فتح ملف EPUB

أولاً، أنشئ `FileInputStream` يشير إلى ملف `.epub` المصدر. إبقاء الدفق مفتوحًا حتى انتهاء التحويل يمنع أخطاء “صفحة فارغة”.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

### الخطوة 2: تعريف خيارات حفظ PDF

`PdfSaveOptions` هي فئة التكوين في Aspose.HTML التي تتحكم في إعدادات إخراج PDF مثل حجم الصفحة، لون الخلفية، والهوامش.  
`Length.fromPixels` يحول بكسلات الشاشة إلى نقاط PDF (1 نقطة = 1/72 بوصة)، مما يتيح لك تحديد الأبعاد بوحدات البكسل المألوفة.

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

#### نصيحة احترافية:
- **البكسل مقابل النقاط:** `Length.fromPixels` يحول بكسلات الشاشة إلى نقاط PDF (1 نقطة = 1/72 بوصة). اختر القيم التي تعكس الحجم المطبوع النهائي الذي تحتاجه.

### الخطوة 3: تحويل EPUB إلى PDF

مع وجود تدفق الإدخال والخيارات المخصصة جاهزة، استدعِ المحول. سيتم حفظ PDF الناتج في الموقع الذي تحدده، مع الحفاظ على أبعاد الصفحة الدقيقة التي حددتها.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

`PdfSaveOptions.setEnableParallelProcessing` هي طريقة تُفعِّل المعالجة المتوازية للصفحات أثناء تحويل PDF.

## الكود الكامل

المثال الكامل القابل للتنفيذ يجمع الخطوات الثلاثة السابقة في فئة Java واحدة. استبدل مسارات العناصر النائبة بمواقع ملفاتك الخاصة.

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|-------|-----|
| **صفحات PDF فارغة** | تم إغلاق تدفق الإدخال قبل التحويل | احتفظ بكتلة `try‑with‑resources` مفتوحة حتى بعد `convertEPUB`. |
| **أبعاد الصفحة غير صحيحة** | استخدام بكسلات لا تتطابق مع حجم الطباعة المطلوب | حوّل البوصات المطلوبة إلى نقاط (`1 inch = 72 points`) ثم إلى بكسلات باستخدام `Length.fromPixels`. |
| **خطوط مفقودة** | الخطوط غير مدمجة في EPUB | تأكد من أن الخطوط مضمَّنة داخل EPUB أو قم بتثبيتها على الجهاز المضيف. |
| **تباطؤ الأداء في الكتب الكبيرة** | عرض كل صفحة على التوالي | فعّل العرض متعدد الخيوط عبر `PdfSaveOptions.setEnableParallelProcessing(true)` لمعالجة أسرع لملفات EPUB التي تتجاوز 500 صفحة. |

## الأسئلة المتكررة (FAQs)

**س: هل Aspose.HTML for Java مكتبة مجانية؟**  
A: Aspose.HTML for Java هي مكتبة تجارية، ولكن يمكنك الحصول على نسخة تجريبية مجانية من [الموقع](https://releases.aspose.com/).

**س: ما صيغ EPUB المدعومة للتحويل؟**  
A: Aspose.HTML for Java يدعم EPUB 2.0، EPUB 3.0، وEPUB 3.1، ويتعامل مع الكتب القابلة لإعادة التدفق والثابتة مع دعم كامل لـ CSS.

**س: هل يمكنني تخصيص مخرجات PDF أكثر؟**  
A: نعم، يمكنك تخصيص مخرجات PDF عن طريق تعديل إعدادات الصفحة، لون الخلفية، مستوى الضغط، وإعدادات أخرى في `PdfSaveOptions`.

**س: هل هناك أي قيود على نسخة التجربة من Aspose.HTML for Java؟**  
A: قد تضيف نسخة التجربة علامة مائية إلى الصفحات القليلة الأولى وتحدّ من الحد الأقصى لحجم الملف إلى 10 ميغابايت؛ اشترِ ترخيصًا لإزالة هذه القيود.

**س: أين يمكنني الحصول على دعم Aspose.HTML for Java؟**  
A: يمكنك العثور على إجابات لأسئلتك وطلب الدعم في [منتدى Aspose.HTML](https://forum.aspose.com/).

---

**آخر تحديث:** 2026-05-30  
**تم الاختبار مع:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**المؤلف:** Aspose

## دروس ذات صلة

- [ضبط حجم صفحة PDF باستخدام Aspose.HTML for Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [كيفية تحويل EPUB إلى PDF باستخدام Java – باستخدام Aspose.HTML](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-pdf/)
- [تحويل EPUB إلى PDF وصور باستخدام Aspose.HTML for Java](/html/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}