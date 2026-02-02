---
date: 2026-02-02
description: تعلم كيفية ضبط حجم صفحة PDF، وتحويل HTML إلى PDF، وإنشاء PDF من HTML
  باستخدام Aspose.HTML للـ Java. تحكم بسهولة في أبعاد الصفحة.
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: ضبط حجم صفحة PDF باستخدام Aspose.HTML للـ Java
url: /ar/java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ضبط حجم صفحة PDF باستخدام Aspose.HTML للـ Java

إنشاء ملفات PDF من HTML يُعدّ طلبًا شائعًا للتقارير والفواتير والكتب الإلكترونية. عندما **تضبط حجم صفحة PDF** تضمن أن المستند النهائي يطابق التخطيط الذي صممته في HTML، ويمكنك بسهولة **تحويل HTML إلى PDF** بالأبعاد الدقيقة التي تحتاجها. في هذا الدرس ستتعلم كيفية تحويل HTML إلى PDF، ضبط أبعاد مخصصة، والتحكم فيما إذا كانت الصفحة تتوسع تلقائيًا لتناسب أوسع محتوى. سنستعرض مثالًا عمليًا كاملًا باستخدام Aspose.HTML للـ Java.

## إجابات سريعة
- **ماذا يعني “ضبط حجم صفحة PDF”؟** يتيح لك تحديد عرض وارتفاع كل صفحة PDF أو السماح للعارض بأن يتناسب تلقائيًا مع أوسع عنصر.  
- **ما المكتبة المستخدمة؟** Aspose.HTML للـ Java (أحدث إصدار).  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للتطوير؛ يلزم ترخيص تجاري للإنتاج.  
- **هل يمكنني تغيير الأبعاد برمجيًا؟** نعم – استخدم `PageSetup` وخصية `AdjustToWidestPage`.  
- **هل هذا متوافق مع Java 8+؟** بالتأكيد – الواجهة البرمجية تعمل مع أي JDK 8 أو أحدث.

## ما هو “ صفحة PDF يعني تكوين أبعاد كل صفحة ينتجها عارض HTML. يمكنك تحديد حجم ثابت (مثل A4 أو Letter) أو السماح للعارض بحساب العرض الأمثل بناءً على المحتوىقيم، والدقة البصرية.

## لماذا ضبط حجم صفحة PDF عند تحويل HTML إلى PDF؟
- **الحفاظ على نية التصميم:** منع قطع المحتوى أو تمدده.  
- **تحسين الطباعة:** مطابقة حجم الورق المطلوب في العمليات اللاحقة.  
- **تحسين القراءة:** تجنب المساحات البيضاء الزائدة أو النص المتقارب.  
- **المستندات الديناميكية:** ملاءمة الجداول أو الصور العريضة تلقائيًا دون حسابات يدوية.

## متى يجب استخدام هذا النهج؟
إذا كنت تُنشئ فواتير، كتالوجات منتجات، أو أدلة تقنية حيث يجب أن يبقى التخطيط ثابتًا عبر الأجهزة والطابعات، فإن ضبط حجم صفحة PDF يضمن أن النتيجة تبدو تمامًا كما هو مقصود. كما أنه مفيد عندما تحتوي المستندات على ج ذلك.

## المتطلبات المسبقة
قبل البدء، تأكد من وجود:

- **Java Development Kit (JDK) 8 أو أعلى** مثبت على جهازك.  
- **Aspose.HTML للـ Java** – حمّل أحدث ملف JAR من [صفحة الإصدار الرسمية](https://releases.aspose.com/html/java/).  
- **ملف HTML** تريد تحويله (سنستخدم `FirstFile.html` في المثال).  

## استيراد الحزم
أولاً، استورد الفئات التي سنحتاجها. هذه الكتلة لا تتغير عن الدرس الأصلي.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## الخطوة 1: قراءة محتوى HTML
نقرأ الخام للمعالجة اللاحقة.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## الخطوة 2: كتابة (وتغذية) HTML
هنا نقوم بنسخ ملف HTML الأصلي إلى ملف جديد ونضيف بعض الأنماط المضمنة لتوضيح كيف يؤثر التنسيق على مخرجات PDF. يمكنك استبدال CSS النموذجي بخصائصك الخاصة.

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
الآن سنستعرض كيفية** باستخدام استراتيجيتين مختلفتين لحجم الصفحة.

### 3.1 حجم الصفحة غير مُضبط لعرض المحتوى
في هذه الحالة تجاوز أي عنصر هذه الحدود، سيتم قصه.

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

 لعرض المحتوى
هنا نفعّل `AdjustToWidestPage`، فيقوم العارض بتوسيع عرض الصفحة تلقائيًا لاستيعاب أوسع عنصر مع الحفاظ على الارتفاع ثابتًا.

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

## المشكلات الشائعة & نصائح
| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| يتم قطع المحتوى | الحجم الثابت صغيرidestPage`. |
| النص يبدو غير واضح | DPI الافتراضي منخفض | استخدم `PdfRenderingOptions.setResolution(int dpi)` لزيادة الجودة. |
| الأنماط مفقودة | CSS خارجي غير محمّل | دمج CSS داخل المستند أو استخدم `HTMLDocument.setBaseUrl()` لتوجيهه إلى مجلد الأنماط. |
| ملفات HTML الكبيرة تسبب OutOfMemoryError | العارض يحمل المستند بالكامل في الذاكرة | عالج المستند على أجزاء أو زد حجم heap للـ JVM (`-Xmx`). |

### نصيحة احترافية
عند التعامل مع صور عالية الدقة، اضبط DPI إلى 300 أو أعلى للحفاظ على وضوح الصورة في PDF النهائي.

## الأسئلة المتكررة

**س: ما هو Aspose.HTML للـ Java؟**  
ج: هو مكتبة Java تتيح لك إنشاء، تعديل، وعرض مستندات HTML، بما في ذلك التحويل إلى PDF، PNG، وصيغ أخرى.

**س: كيف يمكنني ضبط حجم صفحة PDF عند تحويل HTML إلى PDF باستخدام Aspose.HTML للـ Java؟**  
ج: استخدم الفئة `PageSetup` واضبط `AdjustToWidestPage` إلى `true` (توسيع تلقائي) أو `false` (حجم ثابت). ثم عيّن الحجم المطلوب عبر `new Page(new Size(width, height))`.

**س: هل يمكنني تخصيص تنسيق محتوى HTML قبل تحويله إلى PDF؟**  
ج: نعم – يمكنك حقن CSS، تعديل DOM، أو استخدام ملفات نمط خارجية. يوضح الدرس حقن CSS داخلية.

**س: أين يمكنني العثور على وثائق Aspose.HTML للـ Java؟**  
ج: الوثائق الشاملة متاحة [هنا](https://reference.aspose.com/html/java/).

**س: هل هناك نسخة تجريبية مجانية متاحة لـ Aspose.HTML للـ Java؟**  
ج: بالتأكيد – حمّل نسخة تجريبية من [صفحة الإصدار](https://releases.aspose.com/html/java/).

## الخلاصة
أنت الآن تعرف **كيفية ضبط حجم صفحة PDF**، **تحويل HTML إلى PDF**، و**تحديد أبعاد PDF مخصصة** باستخدام Aspose.HTML للـ Java. جرّب أحجام صفحات مختلفة، إعدادات DPI، وتعديلات CSS لتصل إلى النتيجة المثالية لحالتك. إذا واجهت أي صعوبات، راجع الوثائق الرسمية أو منتديات دعم Aspose.

---

**آخر تحديث:** 2026-02-02  
**تم الاختبار مع:** Aspose.HTML للـ Java 24.12 (أحدث إصدار)  
**المؤلف:** Aspose  
**الموارد ذات الصلة:** [مرجع API](https://reference.aspose.com/html/java/) | [تحميل نسخة تجريبية مجانية](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}