---
category: general
date: 2026-04-12
description: تعلم كيفية تعيين حجم صفحة PDF وتضمين الخطوط عند تحويل EPUB إلى PDF في
  جافا باستخدام Aspose.HTML. يوضح لك هذا الدليل سير العمل الكامل لتحويل EPUB إلى PDF
  باستخدام جافا.
draft: false
keywords:
- set pdf page size
- embed fonts pdf
- convert epub to pdf
- java epub to pdf
- custom pdf page size
og_description: تعلم كيفية ضبط حجم صفحة PDF وتضمين الخطوط عند تحويل EPUB إلى PDF في
  Java باستخدام Aspose.HTML.
og_title: تعيين حجم صفحة PDF وإدراج الخطوط لتحويل EPUB إلى PDF في Java
tags:
- Java
- PDF
- EPUB
title: تعيين حجم صفحة PDF وإدراج الخطوط لتحويل EPUB إلى PDF في Java
url: /ar/java/converting-epub-to-pdf/how-to-embed-fonts-when-converting-epub-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين حجم صفحة PDF وتضمين الخطوط لتحويل EPUB إلى PDF في Java

إذا كنت بحاجة إلى **set PDF page size** أثناء **convert EPUB to PDF** وتريد ضمان أن المستند الناتج يبدو تمامًا مثل المصدر، فأنت في المكان الصحيح. في هذا الدرس سنستعرض مثالًا كاملاً وجاهزًا للإنتاج بلغة Java يوضح كيفية **embed fonts pdf**، اختيار **custom pdf page size**، وتشغيل التحويل باستخدام Aspose.HTML. في النهاية ستحصل على برنامج جاهز للتنفيذ ينتج PDF دقيق في كل مرة.

## إجابات سريعة
- **ما هو الهدف الرئيسي؟** Set PDF page size and embed fonts when converting EPUB to PDF in Java.  
- **أي مكتبة يجب أن أستخدم؟** Aspose.HTML for Java (free trial available).  
- **هل أحتاج إلى ترخيص للإنتاج؟** Yes – a license removes the evaluation watermark.  
- **هل يمكنني استخدام حجم صفحة مخصص؟** Absolutely – you can pass exact dimensions or use built‑in enums like A4, LETTER, etc.  
- **ما إصدار Java المطلوب؟** Java 17 or newer is recommended.

### المتطلبات المسبقة
- Java 17+ مثبت.  
- Aspose.HTML for Java مضاف إلى مشروعك (Maven، Gradle، أو JAR يدوي).  
- ملف EPUB تريد تحويله.

> إذا كنت تفضل Gradle، فقط استبدل مقطع Maven بالمعاملات المكافئة لـ Gradle.

---

## لماذا يتم تضمين الخطوط في PDF؟

تضمين الخطوط يثبت التصميم البصري للـ EPUB المصدر، بحيث يتم عرض الـ PDF بشكل صحيح على أي جهاز — حتى إذا لم يكن لدى القارئ الخطوط الأصلية مثبتة. بدون التضمين، قد تعود العناوين إلى الخطوط الافتراضية مثل Arial، مما يفسد التخطيط الذي عملت على إنشائه.

**Pro tip:** إذا كنت تعرف الخطوط الدقيقة المستخدمة في الـ EPUB، فقم بتوجيه Aspose إلى مجلد يحتوي على ملفات `.ttf` أو `.otf` تلك باستخدام `pdfOptions.setFontsFolder("path/to/fonts")`. هذا يسرّع عملية التحويل ويقلل من حجم الملف النهائي.

```java
// Configure PDF save options
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setEmbedFonts(true);               // <-- This line embeds all used fonts
```

---

## كيفية تحويل EPUB إلى PDF في Java – سير العمل الكامل

فيما يلي الحد الأدنى من الكود الضروري، لكنه كامل. يغطي ثلاث خطوات أساسية: تحديد موقع الـ EPUB المصدر، تكوين خيارات PDF (بما في ذلك **set PDF page size**)، واستدعاء التحويل.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfSaveOptions;

public class EpubToPdfDemo {

    public static void main(String[] args) throws Exception {
        // Step 1: Point to your source EPUB file
        String epubPath = "YOUR_DIRECTORY/input.epub";

        // Step 2: Set up PDF save options (embed fonts + page size)
        PdfSaveOptions pdfOptions = new PdfSaveOptions();
        pdfOptions.setEmbedFonts(true);                         // Embed fonts for accurate rendering
        pdfOptions.setPageSize(PdfSaveOptions.PageSize.LETTER); // Set PDF page size to Letter (8.5"x11")

        // Step 3: Perform the conversion
        String outputPdf = "YOUR_DIRECTORY/output.pdf";
        Converter.convert(epubPath, outputPdf, pdfOptions);

        System.out.println("Conversion complete! PDF saved to: " + outputPdf);
    }
}
```

### ما الذي يحدث خلف الكواليس؟

1. **Source EPUB** – `epubPath` يخبر Aspose بمكان قراءة حاوية الـ EPUB.  
2. **PDF Options** – `PdfSaveOptions` يتيح لك تشغيل/إيقاف تضمين الخطوط (`setEmbedFonts`) وتحديد أبعاد الصفحة (`setPageSize`). تعداد `PageSize.LETTER` مفيد للـ US‑letter؛ يمكنك أيضًا اختيار `A4`، `A5`، إلخ.  
3. **Conversion Call** – `Converter.convert` يحلل الـ EPUB، يرسم كل صفحة XHTML إلى صفحة PDF، يطبق الخيارات، ويكتب النتيجة.

الطريقة ترمي استثناءً عامًّا `Exception` للتبسيط؛ في الإنتاج ستلتقط الفئات الفرعية المحددة (مثل `IOException`، `FileNotFoundException`) وتعالجها بشكل ملائم.

---

## كيفية تعيين حجم صفحة PDF للنتيجة

اختيار حجم الصفحة المناسب يؤثر على ترقيم الصفحات، وتكبير الصور، وتخطيط الطباعة. توفر Aspose.HTML تعدادًا ملائمًا، ولكن يمكنك أيضًا تمرير حجم مخصص إذا لم تكن القيم الافتراضية مناسبة لاحتياجاتك.

```java
// Example: Custom size – 6" x 9"
pdfOptions.setPageSize(new PdfSaveOptions.PageSize(6.0, 9.0));
```

**When would you need a custom size?**  
ربما تقوم بإنشاء كتب إلكترونية بحجم الجيب، كتيب قابل للطباعة، أو تقرير يتبع حجم قص معين. تقبل الـ API البوصات (أو يمكنك التحويل من المليمترات)، مما يمنحك التحكم الكامل.

## مثال عملي كامل (يتضمن اعتماد Maven)

إذا كنت تستخدم Maven، أضف الاعتماد التالي إلى ملف `pom.xml`. هذا يضمن أن فئات `Converter` و `PdfSaveOptions` موجودة في مسار الفئات.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

**ملف المصدر الكامل (`EpubToPdfDemo.java`)**

```java
package com.example.epubtopdf;

import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfSaveOptions;

/**
 * Demonstrates how to embed fonts and set PDF page size while converting an EPUB file to PDF.
 * Run this class from your IDE or via `java -cp <classpath> com.example.epubtopdf.EpubToPdfDemo`.
 */
public class EpubToPdfDemo {

    public static void main(String[] args) {
        try {
            // -----------------------------------------------------------------
            // 1️⃣ Locate the EPUB file
            // -----------------------------------------------------------------
            String epubPath = "C:/Docs/input.epub";

            // -----------------------------------------------------------------
            // 2️⃣ Configure PDF options – embed fonts & choose page size
            // -----------------------------------------------------------------
            PdfSaveOptions pdfOptions = new PdfSaveOptions();
            pdfOptions.setEmbedFonts(true);                         // Embed every font used in the EPUB
            pdfOptions.setPageSize(PdfSaveOptions.PageSize.LETTER); // Letter size (8.5"x11")

            // -----------------------------------------------------------------
            // 3️⃣ Convert and save the PDF
            // -----------------------------------------------------------------
            String outputPdf = "C:/Docs/output.pdf";
            Converter.convert(epubPath, outputPdf, pdfOptions);

            System.out.println("✅ Success! PDF created at: " + outputPdf);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع سطر تأكيد:

```
✅ Success! PDF created at: C:/Docs/output.pdf
```

افتح ملف PDF الناتج في أي عارض (Adobe Reader، Chrome، إلخ) وسترى:

* جميع العناصر النصية تحتفظ بتنسيق الخط الأصلي.  
* أبعاد الصفحة تتطابق مع حجم **Letter** المختار (أو أي حجم مخصص قمت بتحديده).  
* الصور والجداول والروابط التشعبية من الـ EPUB محفوظة.

إذا فحصت خصائص PDF (File → Properties → Fonts)، ستلاحظ أن كل خط مُدرج كـ **Embedded Subset**، مما يؤكد أن استدعاء `setEmbedFonts(true)` قام بعمله.

---

## الأسئلة المتكررة

**س: ماذا لو كان الـ EPUB الخاص بي يستخدم خطًا مخصصًا غير مثبت على الخادم؟**  
ج: ضع ملفات `.ttf` أو `.otf` في مجلد ووجه Aspose إليه باستخدام `pdfOptions.setFontsFolder("path/to/custom/fonts")`. سيقوم المحول بتحميل وتضمين تلك الخطوط تلقائيًا.

**س: هل يمكنني تحويل عدة ملفات EPUB في تشغيل واحد؟**  
ج: نعم. غلف منطق التحويل داخل حلقة، غيّر `epubPath` و `outputPdf` لكل ملف، ويمكنك تشغيل الحلقة بشكل متوازي باستخدام `ExecutorService` لأن Aspose آمن للخطوط المتعددة.

**س: هل هناك حد لحجم الـ EPUB المدخل؟**  
ج: لا يوجد حد صريح، لكن الـ EPUB الضخم (مئات الميجابايت) قد يستهلك ذاكرة كبيرة. زد حجم كومة JVM (`-Xmx2g` أو أكثر) للكتب الضخمة.

**س: كيف أُعطل تضمين الخطوط لتقليل حجم PDF؟**  
ج: استدعِ `pdfOptions.setEmbedFonts(false)`. سيعتمد الـ PDF على الخطوط المثبتة لدى القارئ، مما يقلل حجم الملف لكن قد يغيّر المظهر.

**س: هل أحتاج إلى ترخيص لـ Aspose.HTML؟**  
ج: ترخيص تجريبي مجاني يعمل للاختبار لكنه يضيف علامة مائية. للاستخدام الإنتاجي، اشترِ ترخيصًا وحمّله عبر `License license = new License(); license.setLicense("path/to/license.xml");`.

## الخلاصة

أنت الآن تعرف **how to set PDF page size** و **embed fonts pdf** عندما **convert EPUB to PDF** في Java باستخدام Aspose.HTML. المثال الكامل القابل للتنفيذ أعلاه يجب أن يعمل مباشرةً — فقط استبدل مسارات العناصر النائبة بملفاتك الخاصة.

الخطوات التالية؟ جرّب صيغ صفحات مختلفة مثل **A4** أو حجم مخصص 6×9، استكشف خيارات `PdfSaveOptions` الأخرى (ضغط الصور، توافق PDF/A)، أو أضف صفحة غلاف برمجيًا. النمط نفسه يعمل مع صيغ المصدر الأخرى (HTML، Markdown) لأن Aspose.HTML يتعامل معها بشكل موحد.

برمجة سعيدة، ولتظهر ملفات PDF الخاصة بك دائمًا كما تريد!

![كيفية تضمين الخطوط في تحويل PDF](https://example.com/images/embed-fonts.png "كيفية تضمين الخطوط في تحويل PDF")

---

**آخر تحديث:** 2026-04-12  
**تم الاختبار مع:** Aspose.HTML for Java 23.10  
**المؤلف:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}