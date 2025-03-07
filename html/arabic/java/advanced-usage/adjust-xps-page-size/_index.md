---
title: ضبط حجم الصفحة في XPS باستخدام Aspose.HTML لـ Java
linktitle: ضبط حجم الصفحة في XPS
second_title: معالجة HTML باستخدام Java مع Aspose.HTML
description: تعرف على كيفية ضبط حجم صفحة XPS باستخدام Aspose.HTML لـ Java. يمكنك التحكم في أبعاد إخراج مستندات XPS بسهولة.
weight: 16
url: /ar/java/advanced-usage/adjust-xps-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ضبط حجم الصفحة في XPS باستخدام Aspose.HTML لـ Java


في هذا البرنامج التعليمي، سنرشدك خلال عملية ضبط حجم صفحة XPS باستخدام Aspose.HTML for Java. تتيح لك هذه المكتبة القوية التعامل مع مستندات HTML وتقديمها بتنسيقات مختلفة، بما في ذلك XPS. يعد ضبط حجم الصفحة أمرًا ضروريًا عندما تحتاج إلى التحكم في أبعاد الإخراج لمستند XPS.

## المتطلبات الأساسية

قبل أن نبدأ، تأكد من توفر المتطلبات الأساسية التالية:

1. بيئة تطوير Java: تأكد من تثبيت Java Development Kit (JDK) على نظامك.

2.  مكتبة Aspose.HTML for Java: تحتاج إلى تنزيل مكتبة Aspose.HTML for Java وتضمينها في مشروع Java الخاص بك. يمكنك العثور على المكتبة[هنا](https://releases.aspose.com/html/java/).

3. ملف HTML المدخل: قم بإعداد ملف HTML الذي تريد عرضه وضبط حجم صفحة XPS له. يمكنك استخدام ملف HTML الخاص بك لهذا البرنامج التعليمي.

## استيراد الحزم

أولاً، تحتاج إلى استيراد الحزم اللازمة للعمل مع Aspose.HTML لـ Java. قم بتضمين هذه الحزم في بداية فئة Java الخاصة بك:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## الخطوة 1: تعيين اسم ملف الإدخال

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 في هذه الخطوة، نقوم بقراءة ملف الإدخال HTML الخاص بك باستخدام`FileInputStream`.

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

 تتضمن هذه الخطوة إنشاء`HTMLDocument` وإضافة الأنماط إليه.

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

تتضمن هذه الخطوة تحديد حجم الصفحة وتحديد ما إذا كان سيتم تعديله إلى أوسع صفحة.

## الخطوة 5: عرض الناتج

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

في الخطوة الأخيرة، نقوم بتقديم إخراج XPS باستخدام الخيارات التي تم تكوينها.

## خاتمة

في هذا البرنامج التعليمي، أوضحنا لك كيفية ضبط حجم صفحة XPS باستخدام Aspose.HTML لـ Java. يمكنك التحكم في أبعاد إخراج مستندات XPS الخاصة بك، والتأكد من أنها تلبي متطلباتك المحددة. باستخدام التعليمات البرمجية والخطوات المقدمة، يمكنك بسهولة تنفيذ هذه الميزة في تطبيقات Java الخاصة بك.

 إذا كان لديك أي أسئلة أو تحتاج إلى مزيد من المساعدة، فلا تتردد في زيارة[توثيق Aspose.HTML لـ Java](https://reference.aspose.com/html/java/) أو اطلب المساعدة على[منتدى اسبوس](https://forum.aspose.com/).

## الأسئلة الشائعة

### س1: ما هو Aspose.HTML لـ Java؟

A1: Aspose.HTML for Java هي مكتبة Java تسمح للمطورين بمعالجة مستندات HTML وتحويلها إلى تنسيقات مختلفة، مثل XPS وPDF والصور.

### س2: أين يمكنني تنزيل Aspose.HTML لـ Java؟

 ج2: يمكنك تنزيل مكتبة Aspose.HTML لـ Java من[هذا الرابط](https://releases.aspose.com/html/java/).

### س3: هل هناك نسخة تجريبية مجانية متاحة لـ Aspose.HTML لـ Java؟

 ج3: نعم، يمكنك الحصول على نسخة تجريبية مجانية من Aspose.HTML لـ Java من[هنا](https://releases.aspose.com/).

### س4: كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.HTML لـ Java؟

 أ4: للحصول على ترخيص مؤقت لـ Aspose.HTML لـ Java، قم بزيارة[هذه الصفحة](https://purchase.aspose.com/temporary-license/).

### س5: هل يمكنني الحصول على دعم Aspose.HTML لـ Java؟

 ج5: نعم، يمكنك طلب المساعدة والدعم من مجتمع Aspose على[منتدى اسبوس](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
