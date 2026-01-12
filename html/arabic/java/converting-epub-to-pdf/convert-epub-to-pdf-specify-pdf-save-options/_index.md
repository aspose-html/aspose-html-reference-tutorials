---
date: 2026-01-02
description: تعلم كيفية تحويل EPUB إلى PDF في Java باستخدام Aspose.HTML مع تعيين حجم
  صفحة PDF مخصص وخيارات حفظ PDF أخرى.
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 'حجم صفحة PDF مخصص: تحديد خيارات حفظ PDF من EPUB إلى PDF'
url: /ar/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حجم صفحة PDF مخصص: تحديد خيارات حفظ PDF لتحويل EPUB إلى PDF

## المقدمة

Aspose.HTML for Java يجعل من السهل **تحويل EPUB إلى PDF** ويمنحك التحكم الكامل في الناتج، بما في ذلك ضبط **حجم صفحة PDF مخصص**. في هذا الدليل خطوة بخطوة سنستعرض كل ما تحتاجه—من إعداد بيئتك إلى تعديل `PdfSaveOptions` بحيث يتطابق ملف PDF المُولد مع أبعاد الصفحة الدقيقة التي تحتاجها. سواءً كنت تبني خط أنابيب نشر، أو منصة تعلم إلكتروني، أو تحتاج فقط إلى أتمتة تحويل المستندات، ستجد التقنيات هنا ذات قيمة.

## إجابات سريعة
- **ما هو الهدف الأساسي من هذا البرنامج التعليمي؟** تحويل ملف EPUB إلى PDF مع تطبيق حجم صفحة PDF مخصص.  
- **أي مكتبة تُستخدم؟** Aspose.HTML for Java.  
- **هل أحتاج إلى ترخيص؟** يتوفر نسخة تجريبية مجانية؛ يتطلب الترخيص التجاري للاستخدام في الإنتاج.  
- **هل يمكنني تغيير لون الخلفية؟** نعم، باستخدام `PdfSaveOptions`.  
- **هل Java 8+ مدعومة؟** بالتأكيد—أي بيئة تشغيل Java حديثة تعمل.

## ما هو حجم صفحة PDF مخصص؟

حجم صفحة PDF مخصص يتيح لك تحديد العرض والارتفاع الدقيق لكل صفحة في ملف PDF الناتج، بدلاً من الاعتماد على الأحجام القياسية مثل A4 أو Letter. هذا مفيد بشكل خاص للكتب الإلكترونية، والنشرات، أو أي سيناريو يتطلب أن يتطابق التصميم البصري مع مخطط محدد.

## لماذا نستخدم Aspose.HTML لتحويل EPUB إلى PDF؟

- **دقة عالية:** يحافظ على التخطيطات المعقدة، والخطوط، والصور.  
- **تحكم دقيق:** ضبط حجم الصفحة، الخلفية، الهوامش، والمزيد عبر `PdfSaveOptions`.  
- **متعدد المنصات:** يعمل على Windows وLinux وmacOS باستخدام نفس كود Java.  
- **أداء:** محرك عرض مُحسّن لتحويلات سريعة.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- **بيئة تطوير Java:** JDK 8 أو أحدث مثبتة ومُعَدة.  
- **Aspose.HTML for Java:** حمّل أحدث ملف JAR من الـ[الموقع](https://releases.aspose.com/html/java/).  
- **ملف EPUB:** مستند `.epub` ترغب في تحويله.  

الآن بعد أن أصبح كل شيء جاهزًا، لننتقل إلى خطوات التحويل الفعلية.

## الخطوة 1: فتح ملف EPUB

أولاً، نحتاج إلى فتح ملف EPUB باستخدام `FileInputStream`. سيتم تمرير هذا التدفق إلى المحول لاحقًا.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## الخطوة 2: تعريف خيارات حفظ PDF

هنا نحدد **حجم صفحة PDF المخصص** ولون الخلفية الاختياري. عدّل قيم البكسل لتتناسب مع الأبعاد التي تريدها.

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

### نصيحة احترافية:
- **البكسل مقابل النقاط:** `Length.fromPixels` يحول بكسلات الشاشة إلى نقاط PDF (نقطة واحدة = 1/72 بوصة). اختر القيم التي تعكس الحجم المطبوع النهائي الذي تحتاجه.

## الخطوة 3: تحويل EPUB إلى PDF

مع تدفق الإدخال والخيارات المخصصة جاهزة، استدعِ المحول. سيتم حفظ ملف PDF الناتج في الموقع الذي تحدده.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## الكود الكامل

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
| **صفحات PDF فارغة** | تم إغلاق تدفق الإدخال قبل التحويل | حافظ على فتح كتلة `try‑with‑resources` حتى بعد استدعاء `convertEPUB`. |
| **أبعاد الصفحة غير صحيحة** | استخدام بكسلات لا تتطابق مع حجم الطباعة المطلوب | حوّل البوصات المطلوبة إلى نقاط (`1 inch = 72 points`) ثم إلى بكسلات باستخدام `Length.fromPixels`. |
| **الخطوط مفقودة** | الخطوط غير مضمنة في EPUB | تأكد من أن الخطوط مُعبأة داخل ملف EPUB أو قم بتثبيتها على الجهاز المضيف. |

## الأسئلة المتكررة (FAQs)

### هل Aspose.HTML for Java مكتبة مجانية؟
Aspose.HTML for Java هي مكتبة تجارية، ولكن يمكنك الحصول على نسخة تجريبية مجانية من الـ[الموقع](https://releases.aspose.com/).

### ما صيغ EPUB التي تدعمها عملية التحويل؟
Aspose.HTML for Java تدعم تحويل صيغ EPUB المتنوعة، مما يضمن التوافق مع معظم مستندات EPUB.

### هل يمكنني تخصيص مخرجات PDF أكثر؟
نعم، يمكنك تخصيص مخرجات PDF عن طريق تعديل إعدادات إعداد الصفحة، لون الخلفية، وإعدادات أخرى في `PdfSaveOptions`.

### هل هناك أي قيود على نسخة التجربة من Aspose.HTML for Java؟
قد تحتوي نسخة التجربة على بعض القيود، لذا يُنصح بمراجعة الوثائق للحصول على التفاصيل.

### أين يمكنني الحصول على الدعم لـ Aspose.HTML for Java؟
يمكنك العثور على إجابات لأسئلتك وطلب الدعم عبر منتدى [Aspose.HTML](https://forum.aspose.com/).

---

**آخر تحديث:** 2026-01-02  
**تم الاختبار مع:** Aspose.HTML for Java 24.11 (أحدث نسخة وقت الكتابة)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}