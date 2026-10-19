---
category: general
date: 2026-04-03
description: تحويل HTML إلى PDF باستخدام Aspose.HTML في Java مع حجم صفحة PDF مخصص،
  ضبط هوامش PDF، وتحديد عرض صفحة PDF. تعلم كيفية تحويل HTML بسرعة.
draft: false
keywords:
- convert html to pdf
- custom pdf page size
- set pdf margins
- how to convert html
- set pdf page width
language: ar
og_description: تحويل HTML إلى PDF باستخدام Aspose.HTML في جافا. يوضح هذا الدليل كيفية
  تعيين حجم صفحة PDF مخصص، والهوامش، وعرض الصفحة للحصول على نتائج مثالية.
og_title: تحويل HTML إلى PDF – حجم صفحة مخصص وهوامش في جافا
tags:
- Java
- PDF
- Aspose.HTML
title: تحويل HTML إلى PDF – حجم صفحة مخصص وهوامش في Java
url: /ar/java/conversion-html-to-other-formats/convert-html-to-pdf-custom-page-size-margins-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل HTML إلى PDF – حجم صفحة مخصص وهوامش في Java

هل احتجت يومًا إلى **تحويل HTML إلى PDF** وتساءلت كيف تتحكم في أبعاد الصفحة؟ في هذا الدرس سنرشدك إلى حل كامل جاهز للتنفيذ يوضح كيفية **تحويل HTML إلى PDF** بحجم صفحة PDF *مخصص*، وكيفية **تعيين هوامش PDF**، وحتى كيفية **تعيين عرض صفحة PDF** باستخدام Aspose.HTML for Java.  

إذا كنت تُنشئ فواتير أو تقارير أو كتبًا إلكترونية، فإن هذه التعديلات على التخطيط هي الفارق بين نص عادي غير منسق ومستند مصقول يبدو تمامًا كما تريد.

## ما ستتعلمه

* كيفية إعداد مشروع Maven/Gradle بسيط باستخدام Aspose.HTML.
* لماذا اختيار حجم الصفحة المناسب مهم للطباعة وعرض الشاشة.
* الكود خطوة بخطوة لـ **تحويل HTML إلى PDF** مع تخصيص الارتفاع والعرض والهوامش.
* المشكلات الشائعة (مثل استعلامات CSS المفقودة) وكيفية تجنبها.
* كيفية التحقق من أن PDF تم إنشاؤه بشكل صحيح.

لا تحتاج إلى أي خبرة سابقة مع Aspose — فقط بيئة تطوير Java أساسية والقدرة على تشغيل دالة `main`.

## المتطلبات المسبقة

* **Java 17** (أو أي JDK حديث) مثبت على جهازك.  
* **Aspose.HTML for Java** المكتبة – يمكنك الحصول على أحدث JAR من Maven Central (`com.aspose:aspose-html:23.9` في وقت كتابة هذا الدرس).  
* ملف HTML بسيط (`input.html`) تريد تحويله إلى PDF.  
* اختياري: محرر صور إذا أردت معاينة مخرجات PDF.

> **نصيحة احترافية:** إذا كنت تستخدم Maven، أضف الاعتماد أدناه إلى ملف `pom.xml`. إذا كنت تفضل Gradle، فإن نفس الإحداثيات تعمل مع تكوين `implementation`.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

```groovy
// Gradle
implementation 'com.aspose:aspose-html:23.9'
```

## تحويل HTML إلى PDF – إعداد المشروع

أولًا: أنشئ فئة Java جديدة تسمى `PdfConversionAdvanced`. ستحتوي هذه الفئة على كامل منطق التحويل. الاستيرادات التي تحتاجها مُدرجة في أعلى الملف—لا تتردد في نسخها ولصقها مباشرة.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.converters.pdf.*;

public class PdfConversionAdvanced {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1: Point to the source HTML file you want to convert.
        // -----------------------------------------------------------------
        String inputHtmlPath = "YOUR_DIRECTORY/input.html";

        // -----------------------------------------------------------------
        // Step 2: Create PdfSaveOptions and configure custom page size.
        // -----------------------------------------------------------------
        PdfSaveOptions pdfOptions = new PdfSaveOptions();

        // A5 size in points (1 pt = 1/72 inch). Adjust as needed.
        pdfOptions.setPageWidth(420);   // set pdf page width
        pdfOptions.setPageHeight(595);  // set pdf page height

        // -----------------------------------------------------------------
        // Step 3: Define margins – 10 mm ≈ 28.35 points.
        // -----------------------------------------------------------------
        pdfOptions.setMarginTop(28.35);
        pdfOptions.setMarginBottom(28.35);
        pdfOptions.setMarginLeft(28.35);
        pdfOptions.setMarginRight(28.35);

        // -----------------------------------------------------------------
        // Step 4: Make sure the converter uses the "print" media type.
        // -----------------------------------------------------------------
        pdfOptions.setMediaType("print");

        // -----------------------------------------------------------------
        // Step 5: Perform the conversion.
        // -----------------------------------------------------------------
        String outputPdfPath = "YOUR_DIRECTORY/output.pdf";
        Converter.convert(inputHtmlPath, outputPdfPath, pdfOptions);

        // -----------------------------------------------------------------
        // Step 6: Confirm the file was created.
        // -----------------------------------------------------------------
        System.out.println("PDF created with custom layout at " + outputPdfPath);
    }
}
```

### لماذا هذه الإعدادات مهمة

* **حجم صفحة PDF مخصص** (`setPageWidth` / `setPageHeight`) يتيح لك استهداف A5 أو Letter أو أي أبعاد مخصصة تحتاجها. إذا تخطيت ذلك، فإن Aspose يستخدم A4 افتراضيًا، مما قد يسبب إهدارًا للورق أو كسر التصميم.
* **تعيين هوامش PDF** يضمن أن المحتوى لا يلتصق بحواف الصفحة—وهو أمر حاسم للطابعات التي تتطلب حدودًا غير قابلة للطباعة.
* **نوع الوسائط “print”** يجبر المحرك على تطبيق أي CSS `@media print` قمت بتعريفه، مما يمنحك تحكمًا دقيقًا في الخطوط والألوان والتخطيط الذي يختلف عن عرض الشاشة.

## تعريف حجم صفحة PDF مخصص

إذا كان حجم A4 الافتراضي غير مناسب لمشروعك، يمكنك استخدام أي أبعاد تريدها. المقتطف البرمجي أعلاه يوضح بالفعل تخطيط A5 كلاسيكي، لكن دعنا نستكشف بعض البدائل:

| الحجم | العرض (pt) | الارتفاع (pt) |
|------|------------|------------|
| **Letter** | 612 | 792 |
| **Legal** | 612 | 1008 |
| **Custom 8×10 inches** | 576 | 720 |

لتطبيق حجم مخصص، استبدل القيم الممررة إلى `setPageWidth` و `setPageHeight`. تذكر: **1 نقطة = 1/72 بوصة**، لذا عملية ضرب سريعة ستحصل على الأرقام الصحيحة.

> **ملاحظة:** إذا كنت بحاجة لتبديل من وضعية portrait إلى landscape، فقط قم بتبديل قيم العرض والارتفاع.

## تعيين هوامش PDF لتخطيط دقيق

الهوامش تُعبّر عنها بالنقاط أيضًا. المثال يستخدم **10 مم** (≈ 28.35 pt) على جميع الجوانب. هل تريد تخطيطًا أكثر ضيقًا؟ غيّر الأرقام:

```java
pdfOptions.setMarginTop(14.18);    // 5 mm
pdfOptions.setMarginBottom(14.18);
pdfOptions.setMarginLeft(21.26);   // 7.5 mm
pdfOptions.setMarginRight(21.26);
```

لماذا ذلك؟ غالبًا ما تكون للطابعات مساحة طباعة دنيا—تعيين الهوامش يمنع قص المحتوى. أيضًا، الهوامش المتسقة تعطي PDF مظهرًا احترافيًا، خاصةً عند إنشاء عقود أو شهادات.

## تعديل عرض (وارتفاع) صفحة PDF ديناميكيًا

أحيانًا يحتوي HTML الذي تستقبله على إشارة للعرض مسبقًا (مثلاً، `<div>` مُصمم بـ 800 px). يمكنك حساب عرض PDF المطلوب مباشرةً:

```java
int htmlWidthPx = 800;                     // example from HTML
double pointsPerPixel = 0.75;              // 96 DPI => 0.75 pt per pixel
pdfOptions.setPageWidth(htmlWidthPx * pointsPerPixel);
```

هذه التقنية تضمن أن PDF يعكس التخطيط الأصلي دون تشويه. إنها حيلة مفيدة عندما **تحتاج إلى تحويل HTML** الذي صُمم أصلاً للعرض على الشاشة.

## تشغيل التحويل والتحقق من النتيجة

بعد ضبط كل شيء، شغّل دالة `main`. إذا تم ربط كل شيء بشكل صحيح، سترى:

```
PDF created with custom layout at YOUR_DIRECTORY/output.pdf
```

افتح ملف PDF الناتج في أي عارض (Adobe Reader، Chrome، أو معاينة نظام التشغيل). يجب أن ترى:

* حجم الصفحة الدقيق الذي حددته.
* هوامش موحدة حول المحتوى.
* تطبيق CSS كما لو أن الصفحة مطبوعة (بفضل `setMediaType("print")`).

![مثال على تحويل HTML إلى PDF](https://example.com/convert-html-to-pdf-output.png "مثال على تحويل html إلى pdf")

*نص alt للصورة يتضمن الكلمة المفتاحية الأساسية لتحسين محركات البحث.*

## الحالات الخاصة الشائعة وكيفية التعامل معها

| المشكلة | العَرَض | الحل |
|-------|---------|-----|
| **CSS مفقود** | النص يبدو عاديًا، بدون خطوط أو ألوان. | تأكد من ضبط `pdfOptions.setMediaType("print")`، وأن HTML الخاص بك يربط بملف الأنماط باستخدام مسار مطلق أو يضمّن CSS داخلًا. |
| **قصّ الصور الكبيرة** | تُقَصّ الصور عند حدود الصفحة. | غيّر حجم الصور في HTML أو اضبط `pdfOptions.setImageResolution(300)` لزيادة DPI، ثم عدّل الهوامش. |
| **حروف Unicode غير معروضة** | الرموز الخاصة تظهر كصناديق. | أضف خطًا يدعم هذه الأحرف وارجعه في CSS الخاص بك (`@font-face`). |
| **بطء الأداء على المستندات الكبيرة** | تستغرق عملية التحويل أكثر من 30 ثانية. | استخدم `pdfOptions.setEnableThreading(true)` (إن كان مدعومًا) أو قسّم HTML إلى أجزاء أصغر ثم دمج ملفات PDF لاحقًا. |

## مثال كامل يعمل (الكامل معًا)

إليك الملف الكامل الذي يمكنك وضعه في مشروع جديد. استبدل `YOUR_DIRECTORY` بمسار مجلد فعلي على جهازك.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.converters.pdf.*;

public class PdfConversionAdvanced {
    public static void main(String[] args) throws Exception {

        // Step 1: Source HTML location
        String inputHtmlPath = "C:/pdf-demo/input.html";

        // Step 2: Configure PDF options – custom size and margins
        PdfSaveOptions pdfOptions = new PdfSaveOptions();
        pdfOptions.setPageWidth(420);   // custom pdf page width (A5)
        pdfOptions.setPageHeight(595);  // custom pdf page height (A5)

        // Set margins – 10 mm ≈ 28.35 pt
        pdfOptions.setMarginTop(28.35);
        pdfOptions.setMarginBottom(28.35);
        pdfOptions.setMarginLeft(28.35);
        pdfOptions.setMarginRight(28.35);

        // Ensure print CSS is used
        pdfOptions.setMediaType("print");

        // Step 3: Destination PDF file
        String outputPdfPath = "C:/pdf-demo/output.pdf";

        // Step 4: Perform conversion
        Converter.convert(inputHtmlPath, outputPdfPath, pdfOptions);

        // Step 5: Confirmation
        System.out.println("PDF created with custom layout at " + outputPdfPath);
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}