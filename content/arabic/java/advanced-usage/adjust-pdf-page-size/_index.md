---
title: ضبط حجم صفحة PDF باستخدام Aspose.HTML لـ Java
linktitle: ضبط حجم صفحة PDF
second_title: معالجة Java HTML باستخدام Aspose.HTML
description: تعرف على كيفية ضبط حجم صفحة PDF باستخدام Aspose.HTML لـ Java. قم بإنشاء ملفات PDF عالية الجودة من HTML بسهولة. التحكم في أبعاد الصفحة بشكل فعال.
type: docs
weight: 15
url: /ar/java/advanced-usage/adjust-pdf-page-size/
---

في العصر الرقمي الحالي، تتزايد الحاجة إلى إنشاء ملفات PDF عالية الجودة من محتوى HTML. Aspose.HTML for Java هي مكتبة Java قوية تسمح لك بتحويل مستندات HTML إلى تنسيق PDF دون عناء. سنركز في هذا البرنامج التعليمي على ضبط حجم الصفحة عند تحويل HTML إلى PDF باستخدام Aspose.HTML لـ Java.

## المتطلبات الأساسية

قبل البدء، تأكد من توفر المتطلبات الأساسية التالية:

- بيئة تطوير Java: تأكد من تثبيت Java Development Kit (JDK) على نظامك.
-  Aspose.HTML لـ Java: تحتاج إلى تنزيل Aspose.HTML لـ Java وتثبيته من موقع الويب[هنا](https://releases.aspose.com/html/java/).
- مستند HTML: يجب أن يكون لديك مستند HTML جاهز للتحويل. إذا لم يكن الأمر كذلك، قم بإنشاء واحد أو استخدم ملف HTML موجود.

## حزم الاستيراد

للبدء، تحتاج إلى استيراد الحزم اللازمة للعمل مع Aspose.HTML لـ Java. يوضح مقتطف التعليمات البرمجية التالي كيفية القيام بذلك:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

الآن بعد أن أصبحت لديك المتطلبات الأساسية وقمت باستيراد الحزم الضرورية، دعنا نقسم عملية ضبط حجم صفحة PDF إلى خطوات متعددة:

## الخطوة 1: قراءة محتوى HTML

أولا، تحتاج إلى قراءة محتوى HTML الذي تريد تحويله إلى PDF. في هذا المثال، سوف نقرأ HTML من ملف يسمى "FirstFile.html."

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## الخطوة الثانية: كتابة محتوى HTML

بعد ذلك، ستكتب محتوى HTML إلى ملف يسمى "FirstFileOut.html."

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // قم بإضافة أنماط أو محتوى HTML مخصص هنا
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

## الخطوة 3: تقديم HTML إلى PDF

الآن، سوف تقوم بتحويل محتوى HTML إلى ملف PDF. سنغطي سيناريوهين: الأول حيث لا يتم ضبط حجم الصفحة على عرض المحتوى، والآخر حيث يتم ضبطه.

### حجم الصفحة غير قابل للتعديل

في هذا السيناريو، يتم تعيين حجم الصفحة على عرض وارتفاع ثابتين، مما قد يؤدي إلى اقتصاص المحتوى إذا تجاوز هذه الأبعاد.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// قم بإنشاء مثيل HTMLDocument من ملف HTML
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// ضبط خيارات عرض PDF
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//تقديم الإخراج
pdf_renderer.render(device, html_document);
```

### تم ضبط حجم الصفحة على عرض المحتوى

في هذا السيناريو، يتم ضبط حجم الصفحة وفقًا لعرض المحتوى.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//تقديم الإخراج
pdf_renderer.render(device, html_document);
```

## خاتمة

في هذا البرنامج التعليمي، اكتشفنا كيفية ضبط حجم صفحة PDF عند تحويل HTML إلى PDF باستخدام Aspose.HTML لـ Java. لقد تعلمت المتطلبات الأساسية، وقمت باستيراد الحزم المطلوبة، واتبعت دليلاً خطوة بخطوة لتحقيق هذه المهمة. باستخدام Aspose.HTML for Java، يمكنك التحكم بسهولة في حجم الصفحة لملفات PDF التي تم إنشاؤها، مما يضمن عرض المحتوى الخاص بك على النحو المنشود.

 لا تتردد في تجربة أحجام وإعدادات مختلفة للصفحة لتلبية متطلباتك المحددة. إذا واجهت أية مشكلات أو كانت لديك أسئلة أخرى، فلا تتردد في طلب المساعدة من[Aspose.HTML لوثائق جافا](https://reference.aspose.com/html/java/) أو ال[Aspose منتدى الدعم](https://forum.aspose.com/).

## الأسئلة الشائعة

### س1: ما هو Aspose.HTML لـ Java؟

A1: Aspose.HTML for Java هي مكتبة Java تتيح لك العمل مع مستندات HTML ومعالجتها وتحويلها وعرضها في تنسيقات مختلفة، بما في ذلك PDF.

### س2: كيف يمكنني ضبط حجم صفحة PDF عند تحويل HTML إلى PDF باستخدام Aspose.HTML لـ Java؟

 ج2: يمكنك ضبط حجم صفحة PDF باستخدام`PageSetup` الصف وتحديد`AdjustToWidestPage` الملكية ل`true` أو "خطأ، حسب متطلباتك".

### س3: هل يمكنني تخصيص نمط محتوى HTML قبل تحويله إلى PDF؟

ج3: نعم، يمكنك تخصيص التصميم عن طريق إضافة عناصر CSS وHTML إلى محتوى HTML الخاص بك قبل تحويله إلى PDF، كما هو موضح في البرنامج التعليمي.

### س4: أين يمكنني العثور على الوثائق الخاصة بـ Aspose.HTML لـ Java؟

 ج4: يمكنك الرجوع إلى الوثائق[هنا](https://reference.aspose.com/html/java/) للحصول على معلومات وأمثلة شاملة.

### س5: هل تتوفر نسخة تجريبية مجانية من Aspose.HTML لـ Java؟

 ج5: نعم، يمكنك الوصول إلى الإصدار التجريبي المجاني من Aspose.HTML لـ Java من[هذا الرابط](https://releases.aspose.com/).