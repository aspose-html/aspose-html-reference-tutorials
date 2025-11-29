---
date: 2025-11-29
description: تعلم كيفية تحويل HTML إلى XPS وضبط حجم صفحة XPS باستخدام Aspose.HTML
  للغة Java. تحكم بسهولة في أبعاد الإخراج.
language: ar
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: تحويل HTML إلى XPS وتعديل حجم صفحة XPS باستخدام Aspose.HTML للغة Java
url: /java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل HTML إلى XPS وتعديل حجم صفحة XPS باستخدام Aspose.HTML للـ Java

في هذا البرنامج التعليمي ستكتشف **كيفية تحويل HTML إلى XPS** وتضبط حجم الصفحة الناتج باستخدام Aspose.HTML للـ Java. سواءً كنت تولد تقارير قابلة للطباعة أو فواتير أو مستندات أرشيفية، فإن التحكم في أبعاد XPS يضمن أن يكون الناتج مطابقًا لتوقعاتك. سنستعرض كل خطوة — من إعداد البيئة إلى إنشاء ملف XPS النهائي — حتى تتمكن من دمج هذه القدرة في تطبيقات Java الخاصة بك فورًا.

## إجابات سريعة
- **ماذا يعني “convert HTML to XPS”؟** يقوم بتحويل مستند HTML إلى ملف XPS، مع الحفاظ على التخطيط والتنسيق.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تعمل للتطوير؛ يلزم ترخيص تجاري للإنتاج.  
- **ما نسخة Java المدعومة؟** Java 8 أو أعلى (يوصى بـ JDK 11+).  
- **هل يمكنني تغيير حجم الصفحة؟** نعم – يتيح لك Aspose.HTML تحديد أبعاد مخصصة قبل التحويل.  
- **كم تستغرق عملية التحويل؟** عادةً أقل من ثانية للصفحات القياسية؛ قد تستغرق المستندات الكبيرة وقتًا أطول.

## ما هو تحويل HTML إلى XPS؟
يعني تحويل HTML إلى XPS أخذ ملف ترميز موجه للويب وإنتاج مستند XPS (XML Paper Specification) — وهو تنسيق ثابت التخطيط وجاهز للطباعة يشبه PDF. يكون ذلك مفيدًا عندما تحتاج إلى مستندات عالية الدقة ومستقلة عن الأجهزة للأرشفة أو الطباعة من تطبيقات Java.

## لماذا تعديل حجم صفحة XPS؟
يمنحك تعديل حجم الصفحة التحكم في الأبعاد الفيزيائية للمستند النهائي (مثل A4، Letter، أو ملصقات مخصصة). يمنع التحجيم غير المرغوب فيه، يضمن ملاءمة المحتوى بشكل مثالي، ويمكن أن يقلل حجم الملف بإزالة المساحات البيضاء غير الضرورية.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من توفر المتطلبات التالية:

1. **بيئة تطوير Java** – يجب تثبيت مجموعة تطوير Java (JDK) على نظامك.  
2. **مكتبة Aspose.HTML للـ Java** – قم بتحميل وإدراج مكتبة Aspose.HTML للـ Java في مشروعك. يمكنك العثور على المكتبة [هنا](https://releases.aspose.com/html/java/).  
3. **ملف HTML الإدخالي** – حضّر ملف HTML تريد تحويله وتعديل حجم صفحة XPS له. يمكنك استخدام ملف HTML الخاص بك لهذا البرنامج التعليمي.

## استيراد الحزم

أولاً، استورد الفئات التي ستحتاجها. تتيح لك هذه الحزم الوصول إلى ميزات معالجة المستندات، والتحويل، وإعداد الصفحة.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## الخطوة 1: تعيين اسم ملف الإدخال

اقرأ ملف HTML المصدر باستخدام `FileInputStream`. يمرر هذا الدفق الـ HTML الخام إلى محرك Aspose.HTML.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## الخطوة 2: إنشاء مستند HTML وتعيين الأنماط

أنشئ كائن `HTMLDocument` الذي يمثل المحتوى الذي ستقوم بتحويله. في هذا المثال نقوم أيضًا بحقن كتلة CSS صغيرة لتوضيح التنسيق — يمكنك استبدالها بالعلامات الخاصة بك.

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

## الخطوة 3: إنشاء خيارات تحويل XPS

أنشئ كائن `XpsRenderingOptions` لتخزين جميع الإعدادات التي تؤثر على التحويل من HTML إلى XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## الخطوة 4: تعديل حجم الصفحة

حدد حجم صفحة مخصص (العرض × الارتفاع بالنقاط) وأخبر المحول ما إذا كان يجب أن يتوسع تلقائيًا إلى أوسع صفحة. ضبط `adjustToWidestPage` على `false` يحافظ على الأبعاد الدقيقة التي تحددها.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## الخطوة 5: إنشاء المخرجات

أخيرًا، أنشئ `XpsDevice` باستخدام الخيارات المكوّنة وقم بتحويل مستند HTML. النتيجة هي ملف XPS مكتمل مع أبعاد الصفحة المخصصة التي حددتها.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|---------|-------|------|
| **إخراج XPS فارغ** | لم يتم إغلاق تدفق الإدخال أو أن `HTMLDocument` يشير إلى ملف خاطئ. | تأكد من أن `FileInputStream` ملفوف بشكل صحيح داخل كتلة try‑with‑resources وأن مسار الملف دقيق. |
| **لم يتم تطبيق حجم الصفحة** | تم ترك `adjustToWidestPage` على `true`. | اضبط `pageSetup.setAdjustToWidestPage(false);` كما هو موضح في الخطوة 4. |
| **CSS غير مدعوم** | يدعم Aspose.HTML مجموعة فرعية من CSS. | التزم بتنسيق أساسي، خطوط، وألوان؛ تجنّب المحددات المتقدمة أو CSS Grid. |
| **LicenseException** | تشغيل بدون ترخيص صالح في بيئة الإنتاج. | قم بتطبيق الترخيص المؤقت أو المشتري قبل التحويل (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## الأسئلة المتكررة

**س: ما هو Aspose.HTML للـ Java؟**  
ج: Aspose.HTML للـ Java هي مكتبة Java تسمح للمطورين بمعالجة وتحويل مستندات HTML إلى صيغ مختلفة، مثل XPS، PDF، والصور.

**س: من أين يمكنني تحميل Aspose.HTML للـ Java؟**  
ج: يمكنك تحميل مكتبة Aspose.HTML للـ Java من [هذا الرابط](https://releases.aspose.com/html/java/).

**س: هل تتوفر نسخة تجريبية مجانية لـ Aspose.HTML للـ Java؟**  
ج: نعم، يمكنك الحصول على نسخة تجريبية مجانية من Aspose.HTML للـ Java من [هنا](https://releases.aspose.com/).

**س: كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.HTML للـ Java؟**  
ج: للحصول على ترخيص مؤقت لـ Aspose.HTML للـ Java، زر [هذه الصفحة](https://purchase.aspose.com/temporary-license/).

**س: هل يمكنني الحصول على دعم لـ Aspose.HTML للـ Java؟**  
ج: نعم، يمكنك طلب المساعدة والدعم من مجتمع Aspose على [منتدى Aspose](https://forum.aspose.com/).

**س: هل يمكنني تحويل HTML إلى XPS على خادم بدون واجهة رسومية؟**  
ج: بالتأكيد. يعمل Aspose.HTML في بيئات بدون واجهة GUI؛ فقط تأكد من تكوين بيئة تشغيل Java بشكل صحيح.

**س: هل تدعم المكتبة هوامش صفحة مخصصة؟**  
ج: نعم. استخدم `PageSetup.setMarginTop()`، `setMarginBottom()`، إلخ، قبل ربط `PageSetup` بخيارات التحويل.

## الخلاصة

لقد استعرضنا العملية الكاملة **لتحويل HTML إلى XPS** وتعديل حجم الصفحة باستخدام Aspose.HTML للـ Java. باتباع هذه الخطوات يمكنك إنشاء مستندات XPS جاهزة للطباعة تتطابق مع متطلبات التخطيط الدقيقة الخاصة بك. لا تتردد في تجربة أبعاد صفحات مختلفة، أو أنماط، أو حتى إضافة رؤوس وتذييلات لتناسب احتياجات مشروعك.

إذا كان لديك أي أسئلة أو تحتاج إلى مساعدة إضافية، استكشف [توثيق Aspose.HTML للـ Java](https://reference.aspose.com/html/java/) أو انضم إلى النقاش في [منتدى Aspose](https://forum.aspose.com/).

---

**آخر تحديث:** 2025-11-29  
**تم الاختبار مع:** Aspose.HTML للـ Java 24.11 (أحدث نسخة وقت الكتابة)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}