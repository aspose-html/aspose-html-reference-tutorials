---
title: ضبط حجم صفحة PDF باستخدام Aspose.HTML لـ Java
linktitle: ضبط حجم صفحة PDF
second_title: معالجة HTML باستخدام Java مع Aspose.HTML
description: تعرف على كيفية ضبط حجم صفحة PDF باستخدام Aspose.HTML لـ Java. قم بإنشاء ملفات PDF عالية الجودة من HTML بسهولة. تحكم في أبعاد الصفحة بفعالية.
weight: 15
url: /ar/java/advanced-usage/adjust-pdf-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ضبط حجم صفحة PDF باستخدام Aspose.HTML لـ Java


في العصر الرقمي الحالي، تزداد الحاجة إلى إنشاء ملفات PDF عالية الجودة من محتوى HTML. Aspose.HTML for Java هي مكتبة Java قوية تتيح لك تحويل مستندات HTML إلى تنسيق PDF دون عناء. في هذا البرنامج التعليمي، سنركز على ضبط حجم الصفحة عند تحويل HTML إلى PDF باستخدام Aspose.HTML for Java.

## المتطلبات الأساسية

قبل أن تبدأ، تأكد من توفر المتطلبات الأساسية التالية:

- بيئة تطوير Java: تأكد من تثبيت Java Development Kit (JDK) على نظامك.
-  Aspose.HTML for Java: تحتاج إلى تنزيل Aspose.HTML for Java وتثبيته من موقع الويب[هنا](https://releases.aspose.com/html/java/).
- مستند HTML: يجب أن يكون لديك مستند HTML جاهز للتحويل. إذا لم يكن الأمر كذلك، قم بإنشاء مستند أو استخدم ملف HTML موجودًا.

## استيراد الحزم

للبدء، تحتاج إلى استيراد الحزم اللازمة للعمل مع Aspose.HTML لـ Java. يوضح مقتطف التعليمات البرمجية التالي كيفية القيام بذلك:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

الآن بعد أن وضعت المتطلبات الأساسية واستوردت الحزم اللازمة، دعنا نقسم عملية ضبط حجم صفحة PDF إلى عدة خطوات:

## الخطوة 1: قراءة محتوى HTML

أولاً، عليك قراءة محتوى HTML الذي تريد تحويله إلى PDF. في هذا المثال، سنقرأ HTML من ملف باسم "FirstFile.html".

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## الخطوة 2: كتابة محتوى HTML

بعد ذلك، سوف تكتب محتوى HTML في ملف يسمى "FirstFileOut.html".

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // أضف أنماط HTML أو محتوى مخصصًا هنا
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

## الخطوة 3: تحويل HTML إلى PDF

الآن، ستقوم بتحويل محتوى HTML إلى ملف PDF. سنتناول حالتين: الأولى حيث لا يتم تعديل حجم الصفحة بما يتناسب مع عرض المحتوى، والثانية حيث يتم تعديله.

### حجم الصفحة غير معدّل

في هذا السيناريو، يتم تعيين حجم الصفحة على عرض وارتفاع ثابتين، مما قد يؤدي إلى اقتصاص المحتوى إذا تجاوز هذه الأبعاد.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// إنشاء مثيل HTMLDocument من ملف HTML
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// تعيين خيارات عرض PDF
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//تقديم الناتج
pdf_renderer.render(device, html_document);
```

### تم تعديل حجم الصفحة حسب عرض المحتوى

في هذا السيناريو، يتم تعديل حجم الصفحة وفقًا لعرض المحتوى.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//تقديم الناتج
pdf_renderer.render(device, html_document);
```

## خاتمة

في هذا البرنامج التعليمي، استكشفنا كيفية ضبط حجم صفحة PDF عند تحويل HTML إلى PDF باستخدام Aspose.HTML for Java. لقد تعلمت المتطلبات الأساسية، واستوردت الحزم المطلوبة، واتبعت دليلًا خطوة بخطوة لتحقيق هذه المهمة. باستخدام Aspose.HTML for Java، يمكنك التحكم بسهولة في حجم الصفحة لملفات PDF التي تم إنشاؤها، مما يضمن عرض المحتوى الخاص بك كما هو مقصود.

 لا تتردد في تجربة أحجام الصفحات والإعدادات المختلفة لتلبية متطلباتك المحددة. إذا واجهت أي مشكلات أو كانت لديك أسئلة أخرى، فلا تتردد في طلب المساعدة من[توثيق Aspose.HTML لـ Java](https://reference.aspose.com/html/java/) أو ال[منتدى دعم Aspose](https://forum.aspose.com/).

## الأسئلة الشائعة

### س1: ما هو Aspose.HTML لـ Java؟

A1: Aspose.HTML for Java هي مكتبة Java تسمح لك بالعمل مع مستندات HTML ومعالجتها وتحويلها وتقديمها إلى تنسيقات مختلفة، بما في ذلك PDF.

### س2: كيف يمكنني تعديل حجم صفحة PDF عند تحويل HTML إلى PDF باستخدام Aspose.HTML لـ Java؟

 أ2: يمكنك تعديل حجم صفحة PDF باستخدام`PageSetup` الصف والإعداد`AdjustToWidestPage` الممتلكات ل`true` أو `false، اعتمادًا على متطلباتك.

### س3: هل يمكنني تخصيص تصميم محتوى HTML قبل تحويله إلى PDF؟

ج3: نعم، يمكنك تخصيص التصميم عن طريق إضافة عناصر CSS وHTML إلى محتوى HTML الخاص بك قبل تحويله إلى PDF، كما هو موضح في البرنامج التعليمي.

### س4: أين يمكنني العثور على وثائق Aspose.HTML لـ Java؟

 أ4: يمكنك الرجوع إلى الوثائق[هنا](https://reference.aspose.com/html/java/) للحصول على معلومات شاملة وأمثلة.

### س5: هل هناك نسخة تجريبية مجانية متاحة لـ Aspose.HTML لـ Java؟

 ج5: نعم، يمكنك الوصول إلى نسخة تجريبية مجانية من Aspose.HTML لـ Java من[هذا الرابط](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
