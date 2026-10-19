---
category: general
date: 2026-03-05
description: إنشاء ملف PDF من HTML بسرعة باستخدام Aspose.HTML – ضبط حجم صفحة PDF مخصص،
  تضمين الخطوط، وتعلم كيفية تحويل HTML إلى PDF مع الكود الكامل.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- html to pdf conversion
- custom pdf page size
- embed fonts pdf
language: ar
og_description: إنشاء PDF من HTML باستخدام Aspose.HTML. يوضح هذا الدليل كيفية تعيين
  حجم صفحة PDF مخصص، تضمين الخطوط في PDF، وإجراء تحويل من HTML إلى PDF.
og_title: إنشاء PDF من HTML – حجم صفحة مخصص وخطوط مدمجة
tags:
- Java
- PDF
- Aspose.HTML
title: إنشاء ملف PDF من HTML بحجم صفحة مخصص وخطوط مدمجة
url: /ar/java/conversion-html-to-other-formats/create-pdf-from-html-with-custom-page-size-and-embedded-font/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF من HTML بحجم صفحة مخصص وخطوط مدمجة

هل احتجت يوماً إلى **create PDF from HTML** لكن شعرت بأنك عالق في مرحلة التنسيق؟ لست وحدك. سواء كنت تحول صفحة هبوط تسويقية إلى كتيب قابل للطباعة أو تقوم بأرشفة الفواتير التي تُولد في تطبيق ويب، فمن المحتمل أنك تريد ملف PDF يطابق أبعاد علامتك التجارية بدقة ويحافظ على وضوح كل خط.  

في هذا الدرس سنستعرض مثالاً كاملاً جاهزاً للتنفيذ يوضح كيفية **convert HTML to PDF** باستخدام Aspose.HTML for Java، وتعيين **custom PDF page size**، وتمكين **embed fonts PDF** بحيث يبدو الناتج متطابقاً على أي جهاز. في النهاية ستحصل على فئة Java واحدة يمكنك وضعها في مشروعك والبدء في توليد ملفات PDF فوراً.

## ما ستتعلمه

* كيفية إضافة مكتبة Aspose.HTML إلى مشروع Maven أو Gradle.  
* كيفية تكوين **PdfConversionOptions** لتحديد **custom pdf page size** (8.5 × 11 بوصة في هذه الحالة).  
* كيفية تشغيل **embed fonts pdf** حتى يتم عرض النص بشكل صحيح حتى عندما لا يتوفر الخط الأصلي على النظام المستهدف.  
* كيفية تشغيل **HTML to PDF conversion** وقراءة عدد الصفحات الناتجة.  

بدون حشو، مجرد حل عملي من البداية إلى النهاية يمكنك نسخه ولصقه.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك:

* Java 17 أو أحدث مثبتة (تعمل الواجهة البرمجية مع Java 8+، لكن إصدارات JDK الأحدث تعطي أداءً أفضل).  
* أداة بناء – Maven أو Gradle – لسحب ملف JAR الخاص بـ Aspose.HTML من مستودع Maven Central.  
* ملف HTML (`sample.html`) ترغب في تحويله إلى PDF.  
* قليل من الفضول حول تخطيط صفحات PDF – سنغطي ذلك في الشيفرة.

> **نصيحة احترافية:** إذا لم يكن لديك ملف HTML جاهز، فقط أنشئ واحداً بسيطاً يحتوي على `<h1>` وفقرة؛ سيعمل التحويل بنفس الطريقة.

## الخطوة 1: إضافة Aspose.HTML إلى مشروعك (Convert HTML to PDF)

إذا كنت تستخدم **Maven**، أضف الاعتماد التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- latest at time of writing -->
</dependency>
```

لـ **Gradle**، أضف هذا السطر إلى `build.gradle`:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

هذا السطر الواحد يمنحك كل ما تحتاجه لـ **html to pdf conversion** – الـ `Converter`، وفئات الخيارات، وأدوات الرسم.

## الخطوة 2: تكوين حجم صفحة PDF مخصص (Custom PDF Page Size)

الآن بعد أن أصبحت المكتبة على مسار الفئة (classpath) يمكننا البدء في تشكيل المخرجات. كائن `PdfConversionOptions` يتيح لك تحديد أبعاد الصفحة، الهوامش، وما إذا كان يجب دمج الخطوط. إليك الشيفرة التي تحدد **custom pdf page size** بمقاس 8.5 × 11 بوصة مع هوامش نصف بوصة من كل جانب:

```java
// Step 2: Create PDF conversion options and configure page size, margins, and font embedding
PdfConversionOptions pdfOptions = new PdfConversionOptions();

// Set a custom PDF page size – 8.5 × 11 inches (Letter)
pdfOptions.setPageSize(new SizeF(Unit.inch(8.5), Unit.inch(11)));

// Margins are also expressed in inches; here we use 0.5 in on each side
pdfOptions.setMargins(0.5, 0.5, 0.5, 0.5); // left, top, right, bottom

// Enable font embedding so the PDF looks the same everywhere
pdfOptions.setEmbedFonts(true);
```

لاحظ استدعاء `setEmbedFonts(true)`. هذه العلامة تخبر Aspose.HTML بـ **embed fonts PDF**، مما يلغي مشكلة “الخط المفقود” التي قد تظهر عند فتح ملفات PDF على جهاز مختلف.

## الخطوة 3: تنفيذ تحويل HTML إلى PDF

مع إعداد الخيارات، يصبح التحويل الفعلي سطرًا واحدًا. نوجه الـ `Converter` إلى ملف HTML المصدر وملف PDF الوجهة، ثم نمرر إليه الخيارات التي أنشأناها للتو:

```java
// Step 3: Convert the HTML file to PDF using the configured options
String htmlPath = "YOUR_DIRECTORY/sample.html";
String pdfPath  = "YOUR_DIRECTORY/custom.pdf";

PdfConversionResult conversionResult = Converter.convertHTML(htmlPath, pdfPath, pdfOptions);
```

إذا سارت الأمور بسلاسة، سيحتوي `conversionResult` على بيانات تعريفية حول ملف PDF المُولد، مثل عدد الصفحات.

## الخطوة 4: التحقق من الناتج – فحص عدد الصفحات

من الجيد دائمًا التأكد من أن التحويل نجح. يوفر لك `PdfConversionResult` طريقة سريعة لقراءة عدد الصفحات:

```java
// Step 4: Output the number of pages in the generated PDF
System.out.println("Custom PDF created, pages: " + conversionResult.getPageCount());
```

تشغيل البرنامج يجب أن يطبع شيئًا مشابهًا لـ:

```
Custom PDF created, pages: 1
```

هذا السطر يخبرك أن **html to pdf conversion** أنتج ملف PDF بصفحة واحدة، مطابقًا لـ **custom pdf page size** الذي حددته. إذا كان ملف HTML المصدر أطول، سترى عدد صفحات أكبر تلقائيًا.

## مثال كامل يعمل

فيما يلي الفئة Java الكاملة التي يمكنك نسخها إلى ملف باسم `ConvertHtmlToPdfWithOptions.java`. استبدل `YOUR_DIRECTORY` بالمجلد الفعلي الذي يحتوي على `sample.html`.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.pdf.PdfConversionOptions;
import com.aspose.html.converters.pdf.PdfConversionResult;
import com.aspose.html.drawing.SizeF;
import com.aspose.html.drawing.Unit;

public class ConvertHtmlToPdfWithOptions {
    public static void main(String[] args) throws Exception {

        // Step 1: Create PDF conversion options and configure page size, margins, and font embedding
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(new SizeF(Unit.inch(8.5), Unit.inch(11)));
        pdfOptions.setMargins(0.5, 0.5, 0.5, 0.5);   // left, top, right, bottom (in inches)
        pdfOptions.setEmbedFonts(true);            // embed fonts PDF for consistent rendering

        // Step 2: Convert the HTML file to PDF using the configured options
        String htmlPath = "YOUR_DIRECTORY/sample.html";
        String pdfPath  = "YOUR_DIRECTORY/custom.pdf";
        PdfConversionResult conversionResult = Converter.convertHTML(htmlPath, pdfPath, pdfOptions);

        // Step 3: Output the number of pages in the generated PDF
        System.out.println("Custom PDF created, pages: " + conversionResult.getPageCount());
    }
}
```

### النتيجة المتوقعة

بعد أن تقوم بترجمة الشيفرة (`javac ConvertHtmlToPdfWithOptions.java`) وتشغيل الفئة (`java ConvertHtmlToPdfWithOptions`)، ستجد `custom.pdf` في نفس المجلد. افتحه بأي عارض PDF؛ يجب أن ترى HTML الأصلي مُعرضًا على **custom pdf page size** مع دمج جميع الخطوط بشكل صحيح. لا تحذيرات عن خطوط مفقودة، ولا تحولات في التخطيط.

![إنشاء PDF من مثال HTML يظهر معاينة PDF المُولدة](/images/create-pdf-from-html-preview.png "معاينة إنشاء PDF من HTML")

## أسئلة شائعة وحالات خاصة

**ماذا لو كان ملف HTML الخاص بي يشير إلى CSS أو صور خارجية؟**  
يتبع Aspose.HTML نفس القواعد التي يتبعها المتصفح. طالما أن المسارات مطلقة أو نسبية لموقع ملف HTML، سيقوم المحول بجلبها. بالنسبة لعناوين URL البعيدة، تأكد من أن الجهاز الذي يجري التحويل لديه اتصال بالإنترنت.

**هل يمكنني تغيير اتجاه الصفحة إلى landscape؟**  
بالطبع. فقط قم بتبديل قيم العرض والارتفاع عند استدعاء `setPageSize`:

```java
pdfOptions.setPageSize(new SizeF(Unit.inch(11), Unit.inch(8.5)));
```

**هل أحتاج إلى ترخيص Aspose.HTML للاستخدام في الإنتاج؟**  
تعمل المكتبة في وضع التقييم، لكنها تضيف علامة مائية إلى ملف PDF. للمشاريع التجارية ستحتاج إلى ملف ترخيص صالح – ببساطة حمّله في بداية برنامجك باستخدام `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`.

**ماذا عن الخطوط Unicode؟**  
إذا كان HTML الخاص بك يحتوي على أحرف غير لاتينية، تأكد من أن الخطوط التي تقوم بدمجها تدعم تلك النقاط الرمزية. ضبط `setEmbedFonts(true)` سيضمن دمج ملف الخط بالكامل، وبالتالي سيعرض PDF Unicode بشكل صحيح على أي جهاز.

## الخلاصة

أنت الآن تعرف بالضبط كيف **create PDF from HTML** مع التحكم في **custom pdf page size** وضمان أن المستند النهائي **embed fonts PDF** لتقديم عرض خالٍ من الأخطاء عبر المنصات. يغطي المثال كامل مسار **html to pdf conversion** – من إعداد الاعتماد، مرورًا بتكوين الخيارات، إلى التحقق من الناتج.

هل تريد التعمق أكثر؟ جرّب تجربة:

* **أحجام صفحات متعددة** في مستند واحد (خيارات مختلفة لكل تحويل).  
* **قوالب رأس/تذييل** باستخدام `PdfPageSettings` الخاصة بـ Aspose.HTML.  
* **ميزات الأمان** مثل حماية كلمة المرور (`PdfEncryptionOptions`).  

كل هذه تبني على الأساس نفسه الذي وضعناه الآن، لذا ستكون جاهزًا للتعامل معها بسهولة.

برمجة سعيدة، واستمتع بتحويل صفحات الويب إلى ملفات PDF مصممة بدقة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}