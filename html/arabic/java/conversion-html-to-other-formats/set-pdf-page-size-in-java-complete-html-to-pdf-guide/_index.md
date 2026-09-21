---
category: general
date: 2026-01-07
description: تعيين حجم صفحة PDF أثناء تحويل HTML إلى PDF في Java. تعلم مثالًا كاملاً
  لتحويل HTML إلى PDF باستخدام Java، وإنشاء PDF من HTML ومعالجة الهوامش.
draft: false
keywords:
- set pdf page size
- html to pdf java
- generate pdf from html
- html file to pdf
- html to pdf example
language: ar
og_description: حدد حجم صفحة PDF أثناء تحويل HTML إلى PDF في Java. اتبع هذا المثال
  خطوة بخطوة لتحويل HTML إلى PDF وتعلم كيفية إنشاء PDF من HTML.
og_title: تعيين حجم صفحة PDF في جافا – دليل كامل لتحويل HTML إلى PDF
tags:
- Java
- PDF conversion
- Aspose.HTML
title: تحديد حجم صفحة PDF في جافا – دليل كامل لتحويل HTML إلى PDF
url: /ar/java/conversion-html-to-other-formats/set-pdf-page-size-in-java-complete-html-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ضبط حجم صفحة PDF في جافا – دليل كامل لتحويل HTML إلى PDF

هل احتجت يومًا إلى **ضبط حجم صفحة PDF** عند تحويل ملف HTML إلى PDF باستخدام جافا؟ لست وحدك. معظم المطورين يواجهون نفس المشكلة: أبعاد الصفحة الافتراضية لا تتطابق مع التصميم الذي أنشأوه في المتصفح، والنتيجة تظهر مضغوطة أو متجاوزة.

في هذا الدرس سنستعرض مثالًا **كاملًا لتحويل html إلى pdf java** لا يقتصر فقط على *ضبط حجم صفحة PDF* بل يوضح لك أيضًا كيفية **generate pdf from html**، تعديل الهوامش، وحتى تمكين التوافق مع PDF‑A‑1b. في النهاية ستحصل على برنامج جاهز للتنفيذ يحول `input.html` إلى `output.pdf` بالضبط كما تتوقع.

## ما الذي ستحتاجه

- **Java Development Kit (JDK) 8 أو أحدث** – سنقوم بالترجمة باستخدام `javac`.
- مكتبة **Aspose.HTML for Java** (الكود يستخدم الإصدار 23.10، لكن أي إصدار حديث يعمل).
- ملف **HTML بسيط** تريد تحويله إلى PDF (سنسميه `input.html`).
- بيئة تطوير متكاملة أو محرر نصوص بسيط – عادةً أكتب في IntelliJ، لكن Eclipse أو VS Code أيضًا مناسبة.

> **نصيحة احترافية:** Aspose تقدم ترخيص تجريبي مجاني لمدة 30 يومًا؛ فقط ضع ملفات JAR في مسار المشروع وستكون جاهزًا للبدء.

## الخطوة 1: إضافة Aspose.HTML إلى مشروعك

إذا كنت تستخدم Maven، الصق هذا الاعتماد داخل ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

لـ Gradle، أضف:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

أو، إذا كنت تفضل الطريقة اليدوية، حمّل ملف JAR من موقع Aspose وضعه في مجلد `libs/`، ثم أضفه إلى مسار الـ classpath عند التجميع:

```bash
javac -cp "libs/*" AdvancedConvert.java
```

## الخطوة 2: تحميل مستند HTML المصدر

أولًا ننشئ كائن `HtmlDocument` يشير إلى الملف الذي نريد تحويله. المُنشئ يقبل مسارًا أو عنوان URL، لذا يمكنك تمرير أي شيء يمكن للمكتبة قراءته.

```java
import com.aspose.html.HtmlDocument;

// ...

// Load the HTML file from the local file system
HtmlDocument htmlDoc = new HtmlDocument("YOUR_DIRECTORY/input.html");
```

> **لماذا هذا مهم:** تحميل المستند مسبقًا يمنح المحول شجرة DOM كاملة، وهو أمر أساسي لحسابات التخطيط الدقيقة—خاصة عندما تقوم لاحقًا بـ **set pdf page size**.

## الخطوة 3: تكوين خيارات تحويل PDF (ضبط حجم صفحة PDF)

الآن يأتي جوهر الدرس: تكوين `PdfConversionOptions`. هذا الكائن يتيح لك تحديد حجم الصفحة، الهوامش، وحتى توافق PDF/A. أدناه نستخدم `PdfPageSize.A4` المحدد مسبقًا، لكن يمكنك اختيار أي قيمة من القيم المتاحة في الـ enum (`Letter`, `Legal`, `A3`, إلخ) أو إنشاء حجم مخصص.

```java
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.render.PdfA;
import com.aspose.html.render.PdfPageSize;

// ...

PdfConversionOptions conversionOptions = new PdfConversionOptions();

// Set the desired PDF page size – this is where we *set pdf page size* for the output
conversionOptions.setPageSize(PdfPageSize.A4);          // A4 is 210 × 297 mm
conversionOptions.setMarginTop(10);                    // Top margin in points (≈0.35 mm)
conversionOptions.setMarginBottom(10);                 // Bottom margin in points
conversionOptions.setPdfA(PdfA.Standard.PdfA1b);       // Optional: enforce PDF‑A‑1b compliance
```

### حجم مخصص (إضافة)

إذا لم تكن الأحجام القياسية تناسب تصميمك، يمكنك إنشاء `PdfPageSize` يدويًا:

```java
import com.aspose.html.render.PdfPageSize;

// Width = 8.5 inches, Height = 11 inches (Letter size) in points (1 inch = 72 points)
PdfPageSize customSize = new PdfPageSize(8.5 * 72, 11 * 72);
conversionOptions.setPageSize(customSize);
```

> **حالة حافة:** عندما يحتوي HTML على عناصر أوسع من حجم الصفحة المختار، سيقوم المحول تلقائيًا بتصغيرها. ومع ذلك، ضبط حجم الصفحة المناسب مسبقًا يجنبك التحجيم غير المتوقع.

## الخطوة 4: تنفيذ التحويل

مع تحميل المستند وتكوين الخيارات، يصبح التحويل سطرًا واحدًا فقط. طريقة `Converter.convert` تكتب ملف PDF إلى المسار الذي تحدده.

```java
import com.aspose.html.converters.Converter;

// ...

Converter.convert(htmlDoc, "YOUR_DIRECTORY/output.pdf", conversionOptions);
System.out.println("Conversion complete! PDF saved as output.pdf");
```

إذا شغّلت البرنامج الآن، يجب أن ترى `output.pdf` في المجلد المستهدف، مُنسقًا بحجم **صفحة A4** (أو أي حجم اخترته).

## الخطوة 5: التحقق من النتيجة – قائمة مراجعة سريعة

1. **افتح ملف PDF** في عارض (Adobe Reader، Foxit، إلخ). هل كل صفحة تتطابق مع الأبعاد التي ضبطتها؟
2. **تحقق من الهوامش** – يجب أن تكون الأعلى والأسفل بالضبط 10 نقطة كما عرّفنا.
3. **توافق PDF/A** – إذا فتحت خصائص الملف، ستجد “PDF/A‑1b” مدرجًا تحت قسم “إصدار PDF”.
4. **دقة المحتوى** – قارن PDF المُنتج مع HTML الأصلي في المتصفح. يجب أن تكون النصوص، الصور، وCSS متطابقة.

إذا لاحظت أي اختلاف، عد إلى **الخطوة 3** وعدّل حجم الصفحة أو الهوامش. غالبًا ما تحل التعديلات الصغيرة معظم المشكلات المتعلقة بالتخطيط.

## مثال عملي كامل

فيما يلي الفئة الجاوية الكاملة الجاهزة للتنفيذ. ما عليك سوى استبدال `YOUR_DIRECTORY` بالمسار المطلق حيث يوجد ملف `input.html`.

```java
// AdvancedConvert.java
import com.aspose.html.HtmlDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.render.PdfA;
import com.aspose.html.render.PdfPageSize;

public class AdvancedConvert {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HtmlDocument htmlDoc = new HtmlDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Create PDF conversion options and configure page settings
        PdfConversionOptions conversionOptions = new PdfConversionOptions();
        conversionOptions.setPageSize(PdfPageSize.A4);          // Use A4 paper size
        conversionOptions.setMarginTop(10);                    // Top margin (points)
        conversionOptions.setMarginBottom(10);                 // Bottom margin (points)
        conversionOptions.setPdfA(PdfA.Standard.PdfA1b);       // Enable PDF‑A‑1b compliance

        // Step 3: Convert the HTML document to PDF using the configured options
        Converter.convert(htmlDoc, "YOUR_DIRECTORY/output.pdf", conversionOptions);

        System.out.println("PDF successfully generated with the set page size!");
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع:

```
PDF successfully generated with the set page size!
```

وينشئ `output.pdf` بأبعاد صفحة **210 مم × 297 مم** (A4) مع هوامش علوية/سفلية 10 نقاط.

## أسئلة شائعة وحالات حافة

### “هل يمكنني ضبط الاتجاه أفقيًا (landscape)؟”

نعم. استخدم قيم enum `PdfPageSize` للأحجام الأفقية (`A4_Landscape`, `Letter_Landscape`, إلخ):

```java
conversionOptions.setPageSize(PdfPageSize.A4_Landscape);
```

### “ماذا لو كان HTML يعتمد على CSS أو صور خارجية؟”

تأكد من أن المسارات مطلقة أو أن ملف HTML موجود في نفس المجلد مع الأصول. يقوم المحول بحل عناوين URL النسبية بناءً على موقع ملف HTML.

### “هل يمكن تحويل عدة ملفات HTML دفعة واحدة؟”

غلف منطق التحويل داخل حلقة:

```java
String[] files = {"file1.html", "file2.html"};
for (String f : files) {
    HtmlDocument doc = new HtmlDocument("YOUR_DIRECTORY/" + f);
    Converter.convert(doc, "YOUR_DIRECTORY/" + f.replace(".html", ".pdf"), conversionOptions);
}
```

### “هل أحتاج إلى ترخيص للإنتاج؟”

الترخيص يزيل علامة التقييم التجريبية ويفتح الأداء الكامل. سجّل في Aspose، حمّل ملف الترخيص، وحمّله عند بدء تشغيل التطبيق:

```java
import com.aspose.html.License;
License license = new License();
license.setLicense("Aspose.Total.Java.lic");
```

## الخلاصة

لقد استعرضنا الآن سير عمل **كامل لتحويل html إلى pdf java** يتيح لك **ضبط حجم صفحة PDF** بدقة، التحكم في الهوامش، وحتى إنتاج ملفات متوافقة مع PDF‑A‑1b. المقتطف أعلاه يُعد أساسًا قويًا لأي مشروع جافا يحتاج إلى **generate pdf from html**—سواء كنت تبني فواتير، تقارير، أو كتب إلكترونية.

ما الخطوة التالية؟ جرّب تغيير حجم الصفحة إلى `Letter`، جرب أبعادًا مخصصة، أو أضف رأس/تذييل باستخدام `PdfPageEditor` من Aspose. يمكنك أيضًا استكشاف تحويل مجلد كامل من ملفات HTML، وتحويل موقع ثابت إلى دليل PDF محمول.

هل لديك أسئلة إضافية حول **تحويل html file to pdf**، أو تريد معرفة كيفية تضمين الخطوط؟ اترك تعليقًا، ولنستمر في النقاش. برمجة سعيدة! 

![Diagram showing the conversion flow with set pdf page size](/images/set-pdf-page-size.png "set pdf page size example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}