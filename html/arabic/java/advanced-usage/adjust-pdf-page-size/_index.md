---
date: 2026-03-18
description: تعلم كيفية تعديل حجم صفحة PDF، وتحويل HTML إلى PDF وإنشاء PDF من HTML
  باستخدام Aspose.HTML للغة Java. تحكم في أبعاد الصفحة بسهولة.
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: تعديل حجم صفحة PDF باستخدام Aspose.HTML للـ Java
url: /ar/java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ضبط حجم صفحة PDF باستخدام Aspose.HTML للـ Java

إنشاء ملفات PDF من HTML هو مطلب شائع للتقارير والفواتير والكتب الإلكترونية. عندما **تضبط حجم صفحة PDF** تضمن أن المستند النهائي يطابق التخطيط الذي صممته في HTML. في هذا البرنامج التعليمي ستتعلم كيفية تحويل HTML إلى PDF، وتعيين أبعاد مخصصة، والتحكم فيما إذا كانت الصفحة تتوسع تلقائيًا لتناسب أوسع محتوى. سنستعرض مثالًا عمليًا كاملًا باستخدام Aspose.HTML للـ Java، حتى تتمكن بثقة من **تغيير أبعاد صفحة PDF** في مشاريعك.

## إجابات سريعة
- **ماذا يعني “ضبط حجم صفحة PDF”؟** يسمح لك بتحديد عرض وارتفاع كل صفحة PDF أو السماح للمُعالج بتكييف العرض تلقائيًا ليتناسب مع أوسع عنصر.  
- **ما المكتبة المستخدمة؟** Aspose.HTML for Java (latest version).  
- **هل أحتاج إلى ترخيص؟** الإصدار التجريبي المجاني يكفي للتطوير؛ يتطلب الترخيص التجاري للإنتاج.  
- **هل يمكنني تغيير الأبعاد برمجيًا؟** نعم – استخدم `PageSetup` و الخاصية `AdjustToWidestPage`.  
- **هل هذا متوافق مع Java 8+؟** بالطبع – تعمل الواجهة البرمجية مع أي JDK 8 أو أحدث.

## ما هو “ضبط حجم صفحة PDF”؟
يعني ضبط حجم صفحة PDF تكوين أبعاد كل صفحة ينشئها محول HTML. يمكنك تعيين حجم ثابت (مثل A4 أو Letter) أو السماح للمحول بحساب العرض المثالي بناءً على المحتوى. يمنحك ذلك تحكمًا دقيقًا في التخطيط والترقيم والوفاء البصري.

## لماذا ضبط حجم صفحة PDF عند تحويل HTML إلى PDF؟
- **الحفاظ على نية التصميم:** منع قطع المحتوى أو تمدده.  
- **تحسين الطباعة:** مطابقة حجم الورق المطلوب في العمليات اللاحقة.  
- **تحسين قابلية القراءة:** تجنب المساحات البيضاء الزائدة أو النص الضيق.  
- **المستندات الديناميكية:** تكييف الجداول أو الصور العريضة تلقائيًا دون حسابات يدوية.  

## متى تستخدم “render HTML to PDF” مقابل “generate PDF from HTML”
كلا العبارتين تصفان عملية التحويل نفسها، لكن الصياغة مهمة لاكتشاف البحث. استخدم **render HTML to PDF** عندما تركز على محرك التحويل، واستخدم **generate PDF from HTML** عندما تبرز النتيجة النهائية. في هذا الدليل نغطي كلا السيناريوهين.

## المتطلبات المسبقة
قبل أن تبدأ، تأكد من وجود ما يلي:

- **Java Development Kit (JDK) 8 أو أعلى** مثبت على جهازك.  
- **Aspose.HTML للـ Java** – حمّل أحدث ملف JAR من [صفحة الإصدار الرسمية](https://releases.aspose.com/html/java/).  
- **ملف HTML** تريد تحويله (سنستخدم `FirstFile.html` في المثال).  

## استيراد الحزم
أولاً، استورد الفئات التي سنحتاجها. كتلة الشيفرة أدناه لا تتغير عن البرنامج التعليمي الأصلي.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## الخطوة 1: قراءة محتوى HTML
نقرأ ملف HTML المصدر باستخدام `FileInputStream`. هذه الخطوة تُعدّ العلامات الخام للتلاعب لاحقًا.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## الخطوة 2: كتابة (وتحسين اختياري) HTML
هنا نقوم بنسخ HTML الأصلي إلى ملف جديد ونُدخل بعض الأنماط المضمنة لتوضيح كيف يؤثر التنسيق على مخرجات PDF. لا تتردد في استبدال CSS النموذجي بملفك الخاص.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Add custom HTML styles or content here
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## الخطوة 3: تحويل HTML إلى PDF – سيناريوهان
الآن سنرى كيفية **إنشاء PDF من HTML** باستخدام استراتيجيتين مختلفتين لحجم الصفحة.

### 3.1 حجم الصفحة غير مُضبط لعرض المحتوى
في هذه الحالة نُثَبّت أبعاد الصفحة (100 × 100 نقطة). إذا تجاوز أي عنصر هذه الحدود، سيُقص.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Create an HTMLDocument instance from the HTML file
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Set PDF rendering options
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

### 3.2 حجم الصفحة مُضبط لعرض المحتوى
هنا نُفعّل `AdjustToWidestPage`، بحيث يقوم المحول تلقائيًا بتوسيع عرض الصفحة لاستيعاب أوسع عنصر مع الحفاظ على ارتفاع ثابت.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

## كيفية تعيين أبعاد PDF (كيفية تغيير حجم صفحة PDF) في الشيفرة
كائن `PageSetup` هو المفتاح:

- `setAnyPage(Page page)`: يحدد العرض × الارتفاع الأساسي.  
- `setAdjustToWidestPage(boolean)`: يُبدّل التوسيع التلقائي.  

من خلال تعديل هاتين الخاصيتين يمكنك **تغيير أبعاد صفحة PDF** لأي سيناريو، سواء كنت بحاجة إلى صفحة A4 ثابتة أو عرض ديناميكي يتبع تخطيط HTML الخاص بك.

## المشكلات الشائعة والنصائح
| المشكلة | سبب حدوثها | الحل |
|-------|----------------|-----|
| يتم قطع المحتوى | الحجم الثابت صغير جدًا | زيادة قيم `Size` أو تفعيل `AdjustToWidestPage`. |
| النص غير واضح | دقة DPI الافتراضية منخفضة | استخدم `PdfRenderingOptions.setResolution(int dpi)` لزيادة الجودة. |
| الأنماط مفقودة | لم يتم تحميل CSS الخارجي | ضمّن CSS داخل السطر أو استخدم `HTMLDocument.setBaseUrl()` لتوجيه إلى مجلد ملفات الأنماط. |
| ملفات HTML الكبيرة تسبب OutOfMemoryError | المحول يحمل المستند بالكامل في الذاكرة | عالج المستند على أجزاء أو زد حجم الذاكرة المخصصة للـ JVM (`-Xmx`). |

## نصائح إضافية لضبط حجم صفحة PDF
- **استخدم أحجام الصفحات القياسية** (A4، Letter) بتمرير كائنات `Size` المعرفة مسبقًا من `com.aspose.html.drawing.PaperSize`.  
- **اجمع تعديل العرض مع تعديل الارتفاع** للحفاظ على نسب الأبعاد للصور.  
- **حدد DPI** عندما يكون الإخراج عالي الدقة مطلوبًا، خاصةً للـ PDFs الجاهزة للطباعة.  
- **اختبر مع محتويات مختلفة** (جداول، صور، فقرات طويلة) للتحقق من أن `AdjustToWidestPage` يعمل كما هو متوقع.  

## الأسئلة المتكررة

**س: ما هو Aspose.HTML للـ Java؟**  
ج: هو مكتبة Java تتيح لك إنشاء وتحرير وعرض مستندات HTML، بما في ذلك التحويل إلى PDF، PNG، وصيغ أخرى.

**س: كيف يمكنني ضبط حجم صفحة PDF عند تحويل HTML إلى PDF باستخدام Aspose.HTML للـ Java؟**  
ج: استخدم فئة `PageSetup` واضبط `AdjustToWidestPage` إلى `true` (حجم تلقائي) أو `false` (حجم ثابت). ثم عيّن الـ `Size` المطلوب عبر `new Page(new Size(width, height))`.

**س: هل يمكنني تخصيص تنسيق محتوى HTML قبل تحويله إلى PDF؟**  
ج: نعم – يمكنك إدخال CSS، تعديل DOM، أو استخدام أوراق الأنماط الخارجية. يوضح البرنامج التعليمي إدخال CSS مضمّن.

**س: أين يمكنني العثور على وثائق Aspose.HTML للـ Java؟**  
ج: الوثائق الشاملة متاحة [هنا](https://reference.aspose.com/html/java/).

**س: هل يتوفر نسخة تجريبية مجانية لـ Aspose.HTML للـ Java؟**  
ج: بالتأكيد – حمّل نسخة تجريبية من [صفحة الإصدار](https://releases.aspose.com/html/java/).

## الخلاصة
أنت الآن تعرف كيفية **ضبط حجم صفحة PDF**، **تحويل HTML إلى PDF**، و **تعيين أبعاد PDF مخصصة** باستخدام Aspose.HTML للـ Java. جرّب أحجام صفحات مختلفة، إعدادات DPI، وتعديلات CSS لتحسين النتيجة وفقًا لحالتك الخاصة. إذا واجهت أي صعوبات، راجع الوثائق الرسمية أو منتديات دعم Aspose.

---

**آخر تحديث:** 2026-03-18  
**تم الاختبار مع:** Aspose.HTML for Java (latest)  
**المؤلف:** Aspose  
**الموارد ذات الصلة:** [API Reference](https://reference.aspose.com/html/java/) | [Download Free Trial](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}