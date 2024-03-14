---
title: اضبط حجم صفحة XPS باستخدام Aspose.HTML لـ Java
linktitle: ضبط حجم صفحة XPS
second_title: معالجة Java HTML باستخدام Aspose.HTML
description: تعرف على كيفية ضبط حجم صفحة XPS باستخدام Aspose.HTML لـ Java. يمكنك التحكم في أبعاد الإخراج لمستندات XPS الخاصة بك بسهولة.
type: docs
weight: 16
url: /ar/java/advanced-usage/adjust-xps-page-size/
---

في هذا البرنامج التعليمي، سنرشدك خلال عملية ضبط حجم صفحة XPS باستخدام Aspose.HTML لـ Java. تتيح لك هذه المكتبة القوية التعامل مع مستندات HTML وتقديمها إلى تنسيقات مختلفة، بما في ذلك XPS. يعد ضبط حجم الصفحة أمرًا ضروريًا عندما تحتاج إلى التحكم في أبعاد الإخراج لمستند XPS الخاص بك.

## المتطلبات الأساسية

قبل أن نبدأ، تأكد من توفر المتطلبات الأساسية التالية:

1. بيئة تطوير Java: تأكد من تثبيت Java Development Kit (JDK) على نظامك.

2.  Aspose.HTML لمكتبة Java: أنت بحاجة إلى تنزيل مكتبة Aspose.HTML لـ Java وتضمينها في مشروع Java الخاص بك. يمكنك العثور على المكتبة[هنا](https://releases.aspose.com/html/java/).

3. إدخال ملف HTML: قم بإعداد ملف HTML الذي تريد عرضه وضبط حجم صفحة XPS له. يمكنك استخدام ملف HTML الخاص بك لهذا البرنامج التعليمي.

## حزم الاستيراد

أولاً، تحتاج إلى استيراد الحزم اللازمة للعمل مع Aspose.HTML لـ Java. قم بتضمين هذه الحزم في بداية فصل Java الخاص بك:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## الخطوة 1: قم بتعيين اسم ملف الإدخال

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 في هذه الخطوة، نقرأ ملف إدخال HTML الخاص بك باستخدام ملف`FileInputStream`.

## الخطوة 2: إنشاء مستند HTML وتعيين الأنماط

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 تتضمن هذه الخطوة إنشاء`HTMLDocument` وإضافة الأنماط إليها.

## الخطوة 3: إنشاء خيارات عرض XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

هنا، نقوم بإنشاء خيارات عرض XPS لتكوين عملية العرض.

## الخطوة 4: ضبط حجم الصفحة

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

تتضمن هذه الخطوة ضبط حجم الصفحة وتحديد ما إذا كان سيتم ضبطها على أوسع صفحة.

## الخطوة 5: تقديم الإخراج

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

في الخطوة الأخيرة، نقوم بعرض مخرجات XPS باستخدام الخيارات التي تم تكوينها.

## خاتمة

لقد أوضحنا لك في هذا البرنامج التعليمي كيفية ضبط حجم صفحة XPS باستخدام Aspose.HTML لـ Java. يمكنك التحكم في أبعاد مخرجات مستندات XPS الخاصة بك، مما يضمن أنها تلبي متطلباتك المحددة. باستخدام التعليمات البرمجية والخطوات المقدمة، يمكنك بسهولة تنفيذ هذه الميزة في تطبيقات Java الخاصة بك.

 إذا كان لديك أي أسئلة أو كنت بحاجة إلى مزيد من المساعدة، فلا تتردد في زيارة[Aspose.HTML لوثائق جافا](https://reference.aspose.com/html/java/) أو طلب المساعدة على[منتدى أسبوز](https://forum.aspose.com/).

## الأسئلة الشائعة

### س1: ما هو Aspose.HTML لـ Java؟

A1: Aspose.HTML for Java هي مكتبة Java تسمح للمطورين بمعالجة مستندات HTML وتحويلها إلى تنسيقات مختلفة، مثل XPS وPDF والصور.

### س2: أين يمكنني تنزيل Aspose.HTML لـ Java؟

 ج٢: يمكنك تنزيل مكتبة Aspose.HTML لـ Java من[هذا الرابط](https://releases.aspose.com/html/java/).

### س3: هل تتوفر نسخة تجريبية مجانية من Aspose.HTML لـ Java؟

 ج3: نعم، يمكنك الحصول على نسخة تجريبية مجانية من Aspose.HTML لـ Java من[هنا](https://releases.aspose.com/).

### س4: كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.HTML لـ Java؟

 ج4: للحصول على ترخيص مؤقت لـ Aspose.HTML لـ Java، تفضل بزيارة[هذه الصفحة](https://purchase.aspose.com/temporary-license/).

### س5: هل يمكنني الحصول على دعم لـ Aspose.HTML لـ Java؟

 ج5: نعم، يمكنك طلب المساعدة والدعم من مجتمع Aspose على[منتدى أسبوز](https://forum.aspose.com/).