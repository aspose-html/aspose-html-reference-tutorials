---
category: general
date: 2026-03-26
description: إنشاء ملف PDF بحجم مخصص من HTML باستخدام Aspose.HTML للغة Java. تعلّم
  كيفية تحويل HTML إلى PDF وتحديد حجم صفحة PDF في بضع خطوات فقط.
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- change pdf page size
- generate pdf from html
- set pdf page size
language: ar
og_description: إنشاء ملف PDF بحجم مخصص من HTML باستخدام Aspose. يوضح لك هذا الدليل
  كيفية تحويل HTML إلى PDF، وتغيير حجم صفحة PDF، وتعيين حجم صفحة PDF بسهولة.
og_title: إنشاء حجم مخصص لملف PDF – دليل سريع لتحويل HTML إلى PDF
tags:
- aspose
- java
- pdf
- html
title: إنشاء PDF بحجم مخصص – تحويل HTML إلى PDF باستخدام Aspose
url: /ar/java/conversion-html-to-other-formats/create-pdf-custom-size-convert-html-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء حجم مخصص لملف PDF – تحويل HTML إلى PDF باستخدام Aspose

هل احتجت يومًا إلى **إنشاء حجم مخصص لملف PDF** من ملف HTML؟ في هذا البرنامج التعليمي سنوضح لك كيفية **تحويل HTML إلى PDF** وتعيين حجم صفحة PDF باستخدام Aspose.HTML for Java.  

إذا كنت تقوم بإنشاء فواتير أو تقارير أو كتب إلكترونية، فإن الحصول على أبعاد الصفحة الدقيقة مهم—وإلا سيظهر التخطيط غير مركّز أو سيتم قصه.  

سنستعرض كل خطوة، من تحميل ملف HTML المصدر إلى تعديل الهوامش، وسننتهي بملف PDF جاهز للاستخدام. لا مراجع غامضة، بل مثال كامل قابل للتنفيذ يمكنك نسخه ولصقه اليوم.

## ما ستحتاجه

- **Java 17** (أو أي JDK حديث).  
- **Aspose.HTML for Java** JARs – يمكنك الحصول على أحدث نسخة من مستودع Maven أو موقع Aspose.  
- ملف `input.html` بسيط وضعه في مجلد تملكه.  
- بيئة تطوير متكاملة أو محرر نصوص تختاره؛ عادةً أكتب الكود في IntelliJ IDEA، لكن Eclipse يعمل جيدًا.

وجود هذه المتطلبات يعني أنك لن تواجه أخطاء “class not found” في منتصف العملية.  

الآن، دعنا نغوص في التفاصيل.

![مثال إنشاء حجم مخصص لملف PDF](/images/create-pdf-custom-size.png "لقطة شاشة تُظهر ملف PDF تم إنشاؤه بحجم صفحة مخصص وهوامش – إنشاء حجم مخصص لملف PDF")

## إنشاء حجم مخصص لملف PDF – الخطوات الأساسية

فيما يلي البرنامج الكامل بلغة Java الذي ستحصل عليه. لا تتردد في نسخه إلى ملف يُسمى `ConvertHtmlToPdfCustomPage.java` وتشغيله بعد إضافة تبعيات Aspose إلى مشروعك.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfConversionOptions;
import com.aspose.html.saving.PageSize;
import com.aspose.html.saving.Margin;

public class ConvertHtmlToPdfCustomPage {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Set up PDF conversion options
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(PageSize.A4); // Choose page size (A4, Letter, etc.)
        pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Portrait); // Portrait or Landscape
        pdfOptions.setMargins(new Margin(20, 20, 20, 20)); // Margins: left, top, right, bottom (points)

        // Step 3: Convert the HTML document to a PDF file with the custom settings
        Converter.convertHTML(htmlDoc, "YOUR_DIRECTORY/custom_page.pdf", pdfOptions);

        // Step 4: Inform the user that the PDF has been created
        System.out.println("PDF generated with custom page size and margins.");
    }
}
```

### الخطوة 1 – تحويل HTML إلى PDF: تحميل المستند

أول شيء نفعله هو **تحميل ملف HTML** الذي نريد تحويله إلى PDF.  
`HTMLDocument` يقرأ الملف، يحل الروابط النسبية، ويُنشئ DOM يمكن لـ Aspose عرضه.

> **لماذا هذا مهم:** إذا كان ملف HTML يشير إلى CSS أو صور، سيقوم Aspose بجلبها نسبةً إلى مسار الملف. استخدام مسار مطلق (`YOUR_DIRECTORY/input.html`) يتجنب مفاجآت “file not found”.

### الخطوة 2 – تغيير حجم صفحة PDF: تكوين الخيارات

هنا نقوم بإنشاء كائن `PdfConversionOptions`.  
- `setPageSize(PageSize.A4)` يخبر Aspose باستخدام أبعاد A4 القياسية (210 × 297 مم).  
- `setPageOrientation(...)` يغيّر اتجاه الصفحة إذا كنت تحتاج إلى وضعية أفقية.  
- `setMargins(new Margin(20, 20, 20, 20))` يضيف هامشًا قدره 20 نقطة على كل جانب.

يمكنك استبدال `PageSize.A4` بـ `PageSize.LETTER` أو حتى **حجم مخصص** بتمرير كائن `SizeF`، على سبيل المثال:

```java
pdfOptions.setPageSize(new SizeF(500, 800)); // width, height in points
```

> **نصيحة احترافية:** النقطة الواحدة تساوي 1/72 بوصة. إذا كنت تفكر بالمليمترات، اضرب في 2.83465 للحصول على النقاط.

### الخطوة 3 – إنشاء PDF من HTML: تشغيل التحويل

`Converter.convertHTML` يقوم بالعمل الشاق. يأخذ `HTMLDocument` المحمل، مسار الإخراج، والخيارات التي قمنا بتكوينها.  

إذا أردت **تعيين حجم صفحة PDF** بشكل ديناميكي بناءً على المحتوى، يمكنك حساب الأبعاد المطلوبة قبل هذه الخطوة وتعديل `pdfOptions` وفقًا لذلك.

### الخطوة 4 – التحقق من النتيجة

سطر `System.out.println` اختياري، لكنه يوفر رد فعل سريع عند تشغيل البرنامج من وحدة التحكم. بعد التنفيذ، افتح `custom_page.pdf` – يجب أن ترى ملف PDF بحجم A4 عمودي مع هوامش موحدة قدرها 20 نقطة، تمامًا كما حددنا.

## تحويل HTML إلى PDF – تنويعات شائعة

### استخدام Stream بدلاً من مسار ملف

أحيانًا لا يكون لديك ملف فعلي؛ ربما يأتي HTML من قاعدة بيانات أو API. في هذه الحالة، غلف السلسلة في `ByteArrayInputStream`:

```java
String htmlContent = "<html><body><h1>Hello, PDF!</h1></body></html>";
HTMLDocument htmlDoc = new HTMLDocument(
        new ByteArrayInputStream(htmlContent.getBytes(StandardCharsets.UTF_8)),
        "http://example.com/");
```

المعامل الثاني هو عنوان URL الأساسي لحل الموارد النسبية.

### تغيير اتجاه الصفحة

إذا كان تقريرك عريضًا، غيّر إلى الوضعية الأفقية:

```java
pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Landscape);
```

### ضبط الهوامش بدقة

الهوامش تقبل قيمًا عائمة، لذا يمكنك ضبط 0.5 pt لحافة رفيعة جدًا:

```java
pdfOptions.setMargins(new Margin(5.5, 10.2, 5.5, 10.2));
```

### معالجة ملفات HTML الكبيرة

للمستندات الضخمة، فكر في تمكين **البث الفعال للذاكرة**:

```java
pdfOptions.setUseMemoryCache(true);
```

هذا يخبر Aspose بكتابة البيانات الوسيطة إلى ملفات مؤقتة بدلاً من الاحتفاظ بكل شيء في الذاكرة RAM.

## تعيين حجم صفحة PDF – الحالات الخاصة والمشكلات

- **Missing Fonts:** إذا كان HTML الخاص بك يستخدم خطًا مخصصًا غير مثبت على الخادم، سيتراجع PDF إلى الخط الافتراضي. قم بدمج الخط باستخدام `pdfOptions.getFontEmbeddingMode().setEmbeddingMode(EmbeddingMode.Always);`.  
- **Image Scaling:** الصور عالية الدقة يمكن أن تزيد حجم PDF. استخدم `pdfOptions.setImageResolution(150);` لتقليل الدقة مع الحفاظ على الجودة.  
- **CSS Compatibility:** ليست كل خصائص CSS مدعومة بالكامل. التزم بتقنيات التخطيط القياسية (flexbox يعمل، لكن grid قد يحتوي على بعض العيوب).  
- **Path Permissions:** تأكد من أن العملية لديها صلاحية كتابة إلى `YOUR_DIRECTORY`. وإلا سيتم رمي `IOException`.

## النتيجة المتوقعة

تشغيل البرنامج ينتج ملف PDF يبدو هكذا (توضيح تصوري):

```
+---------------------------------------------------+
|                     Header                        |
|                                                   |
|   (HTML rendered content goes here)               |
|                                                   |
|                     Footer                        |
+---------------------------------------------------+
```

- حجم الصفحة: **A4** (210 × 297 مم).  
- الاتجاه: **عمودي**.  
- الهوامش: **20 pt** على كل جانب.  

افتح الملف بأي عارض PDF (Adobe Reader، Chrome، إلخ) للتأكد.

## الخلاصة

أنت الآن تعرف كيف **تنشئ حجم مخصص لملف PDF** من مصدر HTML باستخدام Aspose.HTML for Java. غطى البرنامج التعليمي كامل العملية: **تحويل HTML إلى PDF**، **تغيير حجم صفحة PDF**، **تعيين حجم صفحة PDF**، و**إنشاء PDF من HTML** مع هوامش مخصصة.  

لا تتردد في التجربة—استبدل `PageSize.LETTER` بحجم قانوني، عدّل الهوامش، أو دمج خطوطك الخاصة. بعد ذلك، قد تستكشف **إضافة علامات مائية**، **تشفير PDF**، أو **معالجة دفعة من ملفات HTML متعددة**. جميع هذه المواضيع تبنى على نفس المفاهيم الأساسية التي غطيناها.  

هل لديك سؤال حول حالة خاصة؟ اترك تعليقًا أدناه، وسأساعدك في حل المشكلة. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}