---
date: 2026-02-04
description: تعلم كيفية إنشاء ملف PDF من HTML عن طريق تعيين ورقة أنماط مخصصة للمستخدم
  في Aspose.HTML للغة Java، وحوّل HTML إلى PDF بسهولة باستخدام خدمة وكيل المستخدم.
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: إنشاء PDF من HTML – تعيين ورقة الأنماط الخاصة بالمستخدم في Aspose.HTML للـ
  Java
url: /ar/java/configuring-environment/set-user-style-sheet/
weight: 16
---

 translation.

Be careful not to translate code placeholders.

Also keep markdown formatting.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF من HTML – تعيين ورقة الأنماط للمستخدم في Aspose.HTML للـ Java

## المقدمة
في هذا الدرس ستتعلم كيفية **إنشاء PDF من HTML** باستخدام Aspose.HTML للـ Java مع تطبيق ورقة أنماط مخصصة للمستخدم.  
هل سبق لك أن رغبت في تعديل مظهر مستندات HTML الخاصة بك بأسلوبك الفريد؟ تخيّل أنك تصمم صفحة ويب وتحتاج إلى جعل العناوين تبرز بلون محدد أو الفقرات تبدو متناسقة عبر الأجهزة. هنا يأتي دور *ورقة الأنماط للمستخدم* و**خدمة وكيل المستخدم (User Agent Service)**. سنستعرض كل خطوة — من كتابة ملف HTML بسيط، ضبط وكيل المستخدم، إلى **تحويل HTML إلى PDF** — لتتمكن من رؤية النتيجة فورًا.

## إجابات سريعة
- **ماذا يعني “إنشاء PDF من HTML”؟** يعني ذلك عرض مستند HTML (مع CSS، صور، خطوط، إلخ) وحفظ المخرجات البصرية كملف PDF.  
- **ما المكوّن المطلوب من Aspose؟** مكتبة Aspose.HTML للـ Java توفر محرك التحويل وخدمة وكيل المستخدم.  
- **هل أحتاج إلى ترخيص للاختبار؟** النسخة التجريبية المجانية تكفي للتطوير؛ يلزم ترخيص تجاري للإنتاج.  
- **هل يمكنني استخدام ملف CSS خارجي؟** نعم – يمكنك ربط أوراق الأنماط الخارجية كما في المتصفح العادي.  
- **كم تستغرق عملية التحويل؟** بالنسبة لمستند بسيط مثل الموجود في هذا الدليل، يكتمل التحويل في أقل من ثانية.

## المتطلبات المسبقة
قبل الغوص في الشيفرة، تأكد من وجود ما يلي:

1. **Aspose.HTML للـ Java** – حمّل أحدث ملف JAR من [صفحة إصدارات Aspose](https://releases.aspose.com/html/java/).  
2. **مجموعة تطوير جافا (JDK) 8+** – تأكد من أن الأمر `java -version` يعرض الإصدار 8 أو أعلى.  
3. **بيئة تطوير متكاملة (IDE)** – IntelliJ IDEA أو Eclipse أو NetBeans جميعها مناسبة.  
4. **معرفة أساسية بـ HTML/CSS** – مفيدة لكنها ليست إلزامية.

## استيراد الحزم
لبدء العمل، استورد الفئات الأساسية في جافا. الاستيراد الوحيد الصريح الذي تحتاجه لهذا المثال هو `java.io.IOException`؛ فالفئات الخاصة بـ Aspose تُستدعى بأسماءها المؤهلة بالكامل لاحقًا.

```java
import java.io.IOException;
```

## الخطوة 1: إنشاء مستند HTML بسيط
أولاً، سنكتب ملف HTML بسيط (`document.html`) سيعمل كمصدر لتحويله إلى PDF.

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **نصيحة احترافية:** احفظ ملف HTML في نفس المجلد الذي يحتوي على ملفات جافا لتجنب مشاكل المسارات.

## الخطوة 2: إعداد تكوين Aspose.HTML
أنشئ كائن `Configuration`. يعمل هذا الكائن كحاوية لجميع الخدمات (بما في ذلك خدمة وكيل المستخدم) التي ستستخدمها لاحقًا.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## لماذا نستخدم خدمة وكيل المستخدم؟
توفر **خدمة وكيل المستخدم** تحكمًا منخفض المستوى في خيارات العرض مثل مجموعة الأحرف الافتراضية، اللغة، الخطوط، والأهم من ذلك في هذا الدرس – ورقة الأنماط المخصصة للمستخدم. من خلال تطبيق الأنماط على هذا المستوى، تضمن مخرجات بصرية متسقة حتى إذا كان HTML الأصلي يفتقر إلى CSS خاص به.

## الخطوة 3: الوصول إلى خدمة وكيل المستخدم  
تتيح لك **خدمة وكيل المستخدم** حقن ورقة أنماط مخصصة، تعيين مجموعة الأحرف الافتراضية، والتحكم في خيارات عرض أخرى.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## الخطوة 4: تعريف وتطبيق ورقة الأنماط للمستخدم  
الآن نُعرّف قواعد CSS التي ستُنسق HTML عند عرضه. هنا نستخدم **خدمة وكيل المستخدم** لتعيين ورقة الأنماط.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **لماذا هذا مهم:** من خلال تطبيق ورقة الأنماط على مستوى وكيل المستخدم، تضمن أن الأنماط تُحترم حتى إذا لم يُشرِ HTML الأصلي إلى ملف CSS.

## الخطوة 5: تحميل مستند HTML مع التكوين المخصص  
مرّر كلًا من مسار الملف وكائن `Configuration` إلى مُنشئ `HTMLDocument`. هذا يربط ورقة الأنماط بالمستند.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## الخطوة 6: تحويل HTML إلى PDF  
بعد أن تم تنسيق المستند بالكامل، استدعِ الطريقة الساكنة `convertHTML` **لتحويل HTML إلى PDF**. يتيح لك كائن `PdfSaveOptions` ضبط مخرجات الملف بدقة (مثل حجم الصفحة، الضغط).

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **النتيجة:** سيحتوي الملف `user-agent-stylesheet_out.pdf` على العنوان باللون البني والفقرات بخلفية GhostWhite، تمامًا كما تم تعريفه في ورقة الأنماط.

## الخطوة 7: تنظيف الموارد  
دائمًا قم بتحرير كائنات Aspose لتفريغ الذاكرة الأصلية.

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

## المشكلات الشائعة والحلول
| المشكلة | السبب | الحل |
|-------|-------|-----|
| **مخرجات PDF فارغة** | لم تُطبق ورقة الأنماط أو لم يُحمَّل المستند باستخدام التكوين. | تأكد من تمرير `configuration` إلى `HTMLDocument` وأنه تم استدعاء `setUserStyleSheet` قبل التحميل. |
| **تحذير خاصية CSS غير مدعومة** | Aspose.HTML لا يدعم بعض خصائص CSS المتقدمة. | استخدم فقط الخصائص المذكورة في وثائق Aspose.HTML أو اعتمد على أنماط أبسط. |
| **FileNotFoundException** | مسار `document.html` غير صحيح. | استخدم مسارًا مطلقًا أو ضع ملف HTML في جذر المشروع. |

## الأسئلة المتكررة

**س: هل يمكنني تطبيق أنماط مختلفة لعناصر HTML مختلفة؟**  
ج: بالتأكيد! يمكنك تعريف عدد غير محدود من قواعد CSS داخل ورقة الأنماط للمستخدم.

**س: ماذا لو احتجت لتغيير ورقة الأنماط ديناميكيًا؟**  
ج: استدعِ `setUserStyleSheet` مرة أخرى قبل إنشاء كائن `HTMLDocument` جديد؛ ستُطبق الأنماط الجديدة في التحويل التالي.

**س: هل يمكن استخدام ملفات CSS خارجية مع Aspose.HTML للـ Java؟**  
ج: نعم – يمكنك إما ربط ورقة أنماط خارجية داخل HTML أو تحميل محتواها وتمريره إلى `setUserStyleSheet`.

**س: كيف يتعامل Aspose.HTML مع خصائص CSS غير المدعومة؟**  
ج: تُتجاهل الخصائص غير المدعومة، مما يسمح للأنماط المتبقية بالعرض دون أخطاء.

**س: هل يمكنني تحويل HTML إلى صيغ أخرى غير PDF؟**  
ج: نعم، يدعم Aspose.HTML التحويل إلى XPS، TIFF، PNG، JPEG، وغيرها باستخدام فئة `SaveOptions` المناسبة.

## الخاتمة
لقد رأيت الآن كيفية **إنشاء PDF من HTML** عن طريق تعيين ورقة أنماط مخصصة للمستخدم باستخدام Aspose.HTML للـ Java. يمنحك هذا الأسلوب تحكمًا كاملاً في المظهر البصري للملف PDF الناتج، مما يجعله مثاليًا لإنشاء تقارير تلقائية، فواتير، أو أي سيناريو يتطلب تنسيقًا ثابتًا. لا تتردد في تجربة CSS أكثر تعقيدًا، خطوط خارجية، أو صيغ تحويل إضافية لتوسيع هذا الأساس.

---

**آخر تحديث:** 2026-02-04  
**تم الاختبار مع:** Aspose.HTML للـ Java 24.11 (أحدث نسخة وقت الكتابة)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}