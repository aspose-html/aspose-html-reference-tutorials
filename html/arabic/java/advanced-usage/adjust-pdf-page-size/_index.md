---
date: 2025-12-01
description: تعلم كيفية تعديل حجم صفحة PDF، وتحويل HTML إلى PDF، وإنشاء PDF من HTML
  باستخدام Aspose.HTML للغة Java. تحكم في أبعاد الصفحة بسهولة.
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: ضبط حجم صفحة PDF باستخدام Aspose.HTML للغة Java
url: /ar/java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ضبط حجم صفحة PDF باستخدام Aspose.HTML للغة Java

## إجابات سريعة
- **ماذا يعني “adjust PDF page size”?** يتيح لك تحديد عرض وارتفاع كل صفحة PDF أو السماح للمُعالج بضبط العرض تلقائيًا ليتناسب مع أوسع عنصر.  
- **ما المكتبة المستخدمة؟** Aspose.HTML للغة Java (أحدث إصدار).  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تعمل للتطوير؛ يتطلب الترخيص التجاري للإنتاج.  
- **هل يمكنني تغيير الأبعاد برمجيًا؟** نعم – استخدم `PageSetup` و الخاصية `AdjustToWidestPage`.  
- **هل هذا متوافق مع Java 8+؟** بالتأكيد – الـ API يعمل مع أي JDK 8 أو أحدث.

## ما هو “adjust PDF page size”؟
ضبط حجم صفحة PDF يعني تكوين أبعاد كل صفحة ينشئها مُعالج HTML. يمكنك تعيين حجم ثابت (مثل A4 أو Letter) أو السماح للمُعالج بحساب العرض الأمثل بناءً على المحتوى. يمنحك ذلك تحكمًا دقيقًا في التخطيط والترقيم والوفاء البصري.

## لماذا ضبط حجم صفحة PDF عند تحويل HTML إلى PDF؟
- **الحفاظ على نية التصميم:** منع قطع المحتوى أو تمدده.  
- **تحسين للطباعة:** مطابقة حجم الورق المطلوب في العمليات اللاحقة.  
- **تحسين قابلية القراءة:** تجنب المساحات البيضاء الزائدة أو النص الضيق.  
- **المستندات الديناميكية:** ضبط العرض تلقائيًا للجداول أو الصور العريضة دون حسابات يدوية.

## المتطلبات المسبقة
قبل البدء، تأكد من وجود ما يلي:

- **Java Development Kit (JDK) 8 أو أعلى** مثبت على جهازك.  
- **Aspose.HTML للغة Java** – حمّل أحدث ملف JAR من [صفحة الإصدار الرسمية](https://releases.aspose.com/html/java/).  
- **ملف HTML** تريد تحويله (سنستخدم `FirstFile.html` في المثال).

## استيراد الحزم
أولاً، استورد الفئات التي سنحتاجها. كتلة الشيفرة أدناه لم تتغير عن البرنامج التعليمي الأصلي.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## الخطوة 1: قراءة محتوى HTML
نقرأ ملف HTML المصدر باستخدام `FileInputStream`. هذه الخطوة تُجهّز العلامات الخام للتعديل لاحقًا.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## الخطوة 2: كتابة (وإثراء اختياري) HTML
هنا نقوم بنسخ ملف HTML الأصلي إلى ملف جديد ونُدخل بعض الأنماط المضمنة لتوضيح كيف يؤثر التنسيق على مخرجات PDF. يمكنك استبدال CSS النموذجي بملفك الخاص.

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

## الخطوة 3: تحويل HTML إلى PDF – سيناريوهين
الآن سنرى كيفية **إنشاء PDF من HTML** باستخدام استراتيجيتين مختلفتين لحجم الصفحة.

### 3.1 حجم الصفحة غير مُضبط لعرض المحتوى
في هذه الحالة نثبت أبعاد الصفحة (100 × 100 نقطة). إذا تجاوز أي عنصر هذه الحدود، سيتم قصه.

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
هنا نُفعّل `AdjustToWidestPage`، بحيث يوسّع المُعالج عرض الصفحة تلقائيًا لاستيعاب أوسع عنصر مع الحفاظ على ارتفاع ثابت.

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

## كيفية ضبط أبعاد PDF (كيفية تغيير حجم صفحة PDF) في الشيفرة
كائن `PageSetup` هو المفتاح:

- `setAnyPage(Page page)`: يحدد العرض × الارتفاع الأساسي.  
- `setAdjustToWidestPage(boolean)`: يبدّل التوسيع التلقائي.  

من خلال تعديل هاتين الخاصيتين يمكنك **ضبط أبعاد PDF** لأي سيناريو، سواء كنت تحتاج إلى صفحة A4 ثابتة أو عرض ديناميكي يتبع تخطيط HTML الخاص بك.

## المشكلات الشائعة والنصائح
| المشكلة | سبب حدوثها | الحل |
|-------|----------------|-----|
| المحتوى يُقَطَع | الحجم الثابت صغير جدًا | زيادة قيم `Size` أو تفعيل `AdjustToWidestPage`. |
| النص يبدو غير واضح | DPI الافتراضي للعرض منخفض | استخدم `PdfRenderingOptions.setResolution(int dpi)` لزيادة الجودة. |
| الأنماط مفقودة | CSS الخارجي غير محمّل | دمج CSS داخل السطر أو استخدم `HTMLDocument.setBaseUrl()` لتوجيه إلى مجلد ملفات الأنماط. |
| ملفات HTML الكبيرة تسبب OutOfMemoryError | المُعالج يحمل المستند بالكامل في الذاكرة | عالج المستند على أجزاء أو زد حجم heap للـ JVM (`-Xmx`). |

## الأسئلة المتكررة

**س: ما هو Aspose.HTML للغة Java؟**  
ج: هي مكتبة Java تتيح لك إنشاء وتحرير وعرض مستندات HTML، بما في ذلك التحويل إلى PDF و PNG وغيرها من الصيغ.

**س: كيف يمكنني ضبط حجم صفحة PDF عند تحويل HTML إلى PDF باستخدام Aspose.HTML للغة Java؟**  
ج: استخدم الفئة `PageSetup` واضبط `AdjustToWidestPage` إلى `true` (حجم تلقائي) أو `false` (حجم ثابت). ثم عيّن الـ `Size` المطلوب عبر `new Page(new Size(width, height))`.

**س: هل يمكنني تخصيص تنسيق محتوى HTML قبل تحويله إلى PDF؟**  
ج: نعم – يمكنك إدخال CSS، تعديل DOM، أو استخدام أوراق الأنماط الخارجية. يوضح البرنامج التعليمي إدخال CSS داخل السطر.

**س: أين يمكنني العثور على وثائق Aspose.HTML للغة Java؟**  
ج: الوثائق الشاملة متوفرة [هنا](https://reference.aspose.com/html/java/).

**س: هل تتوفر نسخة تجريبية مجانية لـ Aspose.HTML للغة Java؟**  
ج: بالتأكيد – حمّل نسخة تجريبية من [صفحة الإصدار](https://releases.aspose.com/html/java/).

## الخلاصة
أنت الآن تعرف كيفية **ضبط حجم صفحة PDF**، **تحويل HTML إلى PDF**، و **تحديد أبعاد PDF مخصصة** باستخدام Aspose.HTML للغة Java. جرّب أحجام صفحات مختلفة، إعدادات DPI، وتعديلات CSS لتحسين المخرجات وفقًا لحالتك الخاصة. إذا واجهت أي تحديات، راجع الوثائق الرسمية أو منتديات دعم Aspose.

---

**آخر تحديث:** 2025-12-01  
**تم الاختبار مع:** Aspose.HTML للغة Java 24.12 (الأحدث)  
**المؤلف:** Aspose  
**الموارد ذات الصلة:** [API Reference](https://reference.aspose.com/html/java/) | [Download Free Trial](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}