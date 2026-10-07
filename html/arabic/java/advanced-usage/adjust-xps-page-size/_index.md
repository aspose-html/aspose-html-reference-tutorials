---
date: 2026-03-18
description: تعلم كيفية تحويل HTML إلى XPS وضبط حجم صفحة XPS باستخدام Aspose.HTML
  للغة Java. تحكم بسهولة في أبعاد الإخراج.
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: تحويل HTML إلى XPS وتعديل حجم صفحة XPS باستخدام Aspose.HTML للغة Java
url: /ar/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل HTML إلى XPS وتعديل حجم صفحة XPS باستخدام Aspose.HTML للغة Java

في هذا الدرس ستكتشف **كيفية تحويل HTML إلى XPS** وتضبط حجم الصفحة الناتج باستخدام Aspose.HTML للغة Java. سواءً كنت تُنشئ تقارير قابلة للطباعة، فواتير، أو مستندات أرشيفية، فإن التحكم في أبعاد XPS يضمن أن المخرجات تظهر تمامًا كما تتوقع. سنستعرض كل خطوة — من إعداد البيئة إلى إنشاء ملف XPS النهائي — حتى تتمكن من دمج هذه القدرة في تطبيقات Java الخاصة بك فورًا.

## إجابات سريعة
- **ماذا يعني “تحويل HTML إلى XPS”؟** يقوم بتحويل مستند HTML إلى ملف XPS مع الحفاظ على التخطيط والتنسيق.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تكفي للتطوير؛ يلزم الحصول على ترخيص تجاري للإنتاج.  
- **ما نسخة Java المدعومة؟** Java 8 أو أعلى (يوصى بـ JDK 11+).  
- **هل يمكنني تغيير حجم الصفحة؟** نعم – يتيح لك Aspose.HTML تحديد أبعاد مخصصة قبل التحويل.  
- **كم تستغرق عملية التحويل؟** عادةً أقل من ثانية للصفحات القياسية؛ قد تستغرق المستندات الكبيرة وقتًا أطول.

## ما هو تحويل HTML إلى XPS؟
تحويل HTML إلى XPS يعني أخذ ملف ترميز ويب وإنتاج مستند XPS (XML Paper Specification) — وهو تنسيق ثابت جاهز للطباعة يشبه PDF. يُفيد ذلك عندما تحتاج إلى مستندات عالية الدقة ومستقلة عن الجهاز للأرشفة أو الطباعة من تطبيقات Java.

## لماذا نضبط حجم صفحة XPS؟
ضبط حجم الصفحة يمنحك التحكم في الأبعاد الفعلية للمستند النهائي (مثل A4، Letter، أو ملصقات مخصصة). يمنع ذلك التحجيم غير المرغوب فيه، يضمن ملاءمة المحتوى تمامًا، ويمكن أن يقلل حجم الملف بإزالة المساحات البيضاء غير الضرورية.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من توفر المتطلبات التالية:

1. **بيئة تطوير Java** – مجموعة تطوير Java (JDK) مثبتة على نظامك.  
2. **مكتبة Aspose.HTML للغة Java** – قم بتحميل وإدراج مكتبة Aspose.HTML للغة Java في مشروعك. يمكنك العثور على المكتبة [هنا](https://releases.aspose.com/html/java/).  
3. **ملف HTML الإدخالي** – حضّر ملف HTML تريد تحويله وضبط حجم صفحة XPS له. يمكنك استخدام ملف HTML الخاص بك لهذا الدرس.

## استيراد الحزم

أولاً، استورد الفئات التي ستحتاجها. تتيح لك هذه الحزم التعامل مع المستندات، التحويل، وميزات إعداد الصفحة.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## دليل خطوة بخطوة

فيما يلي دليل مختصر مرقم يعكس الخطوات الأصلية مع إضافة بعض السياق للوضوح.

### الخطوة 1: تعيين اسم ملف الإدخال

اقرأ ملف HTML المصدر باستخدام `FileInputStream`. يمرر هذا التدفق HTML الخام إلى محرك Aspose.HTML.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### الخطوة 2: إنشاء مستند HTML وتعيين الأنماط

أنشئ كائن `HTMLDocument` الذي يمثل المحتوى الذي ستقوم بتحويله. في هذا المثال نضيف كتلة CSS صغيرة لتوضيح التنسيق — يمكنك استبدالها بالعلامات الخاصة بك.

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### الخطوة 3: إنشاء خيارات تحويل XPS

أنشئ كائن `XpsRenderingOptions` لتخزين جميع الإعدادات التي تؤثر على التحويل من HTML إلى XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### الخطوة 4: ضبط حجم الصفحة  

**كيفية تعيين حجم صفحة XPS** – حدد حجم صفحة مخصص (العرض × الارتفاع بالنقاط) وأخبر المُحوِّل ما إذا كان يجب أن يتوسع تلقائيًا إلى أوسع صفحة. ضبط `adjustToWidestPage` على `false` يحافظ على الأبعاد الدقيقة التي تحددها.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### الخطوة 5: إنشاء المخرجات

أخيرًا، أنشئ كائن `XpsDevice` باستخدام الخيارات المكوَّنة وقم بتحويل مستند HTML. النتيجة هي ملف XPS مكتمل بالأبعاد المخصصة التي حددتها.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|----------------|-----|
| **إخراج XPS فارغ** | عدم إغلاق تدفق الإدخال أو أن `HTMLDocument` يشير إلى ملف غير صحيح. | تأكد من أن `FileInputStream` مغلق ضمن كتلة `try‑with‑resources` وأن مسار الملف صحيح. |
| **عدم تطبيق حجم الصفحة** | ترك `adjustToWidestPage` على `true`. | اضبط `pageSetup.setAdjustToWidestPage(false);` كما هو موضح في الخطوة 4. |
| **CSS غير مدعوم** | Aspose.HTML يدعم مجموعة جزئية من CSS. | التزم بتخطيطات، خطوط، وألوان أساسية؛ تجنّب المحددات المتقدمة أو CSS Grid. |
| **LicenseException** | تشغيل بدون ترخيص صالح في بيئة الإنتاج. | قم بتطبيق الترخيص المؤقت أو المشتراَة قبل التحويل (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## الأسئلة المتكررة

**س: ما هو Aspose.HTML للغة Java؟**  
ج: Aspose.HTML للغة Java هي مكتبة Java تسمح للمطورين بمعالجة وتحويل مستندات HTML إلى صيغ متعددة، مثل XPS، PDF، والصور.

**س: أين يمكنني تحميل Aspose.HTML للغة Java؟**  
ج: يمكنك تحميل مكتبة Aspose.HTML للغة Java من [هذا الرابط](https://releases.aspose.com/html/java/).

**س: هل تتوفر نسخة تجريبية مجانية لـ Aspose.HTML للغة Java؟**  
ج: نعم، يمكنك الحصول على نسخة تجريبية مجانية من [هنا](https://releases.aspose.com/).

**س: كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.HTML للغة Java؟**  
ج: للحصول على ترخيص مؤقت، زر [هذه الصفحة](https://purchase.aspose.com/temporary-license/).

**س: هل يمكنني الحصول على دعم لـ Aspose.HTML للغة Java؟**  
ج: نعم، يمكنك طلب المساعدة من مجتمع Aspose عبر [منتدى Aspose](https://forum.aspose.com/).

**س: هل يمكنني تحويل HTML إلى XPS على خادم بدون واجهة رسومية؟**  
ج: بالتأكيد. يعمل Aspose.HTML في بيئات بدون واجهة GUI؛ فقط تأكد من تكوين بيئة تشغيل Java بشكل صحيح.

**س: هل تدعم المكتبة هوامش صفحة مخصصة؟**  
ج: نعم. استخدم `PageSetup.setMarginTop()`, `setMarginBottom()`، إلخ، قبل إسناد `PageSetup` إلى خيارات التحويل.

## الخلاصة

لقد استعرضنا العملية الكاملة **لتحويل HTML إلى XPS** وتعديل حجم الصفحة باستخدام Aspose.HTML للغة Java. باتباع هذه الخطوات يمكنك إنشاء مستندات XPS جاهزة للطباعة تتطابق تمامًا مع متطلبات التخطيط الخاصة بك. لا تتردد في تجربة أبعاد صفحات مختلفة، أنماط متنوعة، أو حتى إضافة رؤوس وتذييلات لتناسب احتياجات مشروعك.

إذا كان لديك أي أسئلة أو تحتاج إلى مساعدة إضافية، تصفح [توثيق Aspose.HTML للغة Java](https://reference.aspose.com/html/java/) أو انضم إلى النقاش في [منتدى Aspose](https://forum.aspose.com/).

---

**آخر تحديث:** 2026-03-18  
**تم الاختبار مع:** Aspose.HTML للغة Java 24.11 (أحدث نسخة وقت الكتابة)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}