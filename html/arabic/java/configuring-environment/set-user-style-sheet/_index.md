---
date: 2025-12-05
description: تعلم كيفية إنشاء PDF من HTML عن طريق تعيين ورقة أنماط مخصصة للمستخدم
  في Aspose.HTML للـ Java، وتحويل HTML إلى PDF بسهولة باستخدام خدمة وكيل المستخدم.
language: ar
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: إنشاء PDF من HTML – تعيين ورقة الأنماط الخاصة بالمستخدم في Aspose.HTML للغة
  Java
url: /java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF من HTML – تعيين ورقة أنماط المستخدم في Aspose.HTML للـ Java

## مقدمة
في هذا الدرس ستتعلم كيفية **إنشاء PDF من HTML** باستخدام Aspose.HTML للـ Java مع تطبيق ورقة أنماط مخصصة للمستخدم.  
هل وجدت نفسك يومًا ترغب في تعديل مظهر مستندات HTML الخاصة بك بأسلوبك الفريد؟ تخيل أنك تصمم صفحة ويب وتحتاج إلى أن تبرز العناوين بلون محدد أو أن تكون الفقرات متسقة عبر الأجهزة. هنا يأتي دور *ورقة أنماط المستخدم* و **User Agent Service**. سنستعرض كل خطوة — من كتابة ملف HTML بسيط، تكوين وكيل المستخدم، إلى **تحويل HTML إلى PDF** — لتتمكن من رؤية النتيجة فورًا.

## إجابات سريعة
- **ما معنى “إنشاء PDF من HTML”؟** يعني ذلك عرض مستند HTML (مع CSS، الصور، الخطوط، إلخ) وحفظ المخرجات البصرية كملف PDF.  
- **ما المكوّن Aspose المطلوب؟** مكتبة Aspose.HTML للـ Java توفر محرك التحويل وخدمة وكيل المستخدم (User Agent Service).  
- **هل أحتاج إلى ترخيص للاختبار؟** النسخة التجريبية المجانية تعمل للتطوير؛ يلزم ترخيص تجاري للإنتاج.  
- **هل يمكنني استخدام ملف CSS خارجي؟** نعم – يمكنك ربط أوراق الأنماط الخارجية كما في المتصفح العادي.  
- **كم يستغرق التحويل من الوقت؟** بالنسبة لمستند بسيط مثل الموجود في هذا الدليل، يكتمل التحويل في أقل من ثانية.

## المتطلبات المسبقة
قبل أن نغوص في الكود، تأكد من أن لديك ما يلي:

1. **Aspose.HTML للـ Java** – قم بتحميل أحدث ملف JAR من [صفحة إصدارات Aspose](https://releases.aspose.com/html/java/).  
2. **مجموعة تطوير جافا (JDK) 8+** – تأكد من أن الأمر `java -version` يُظهر الإصدار 8 أو أعلى.  
3. **بيئة تطوير متكاملة (IDE)** – IntelliJ IDEA أو Eclipse أو NetBeans ستعمل بشكل جيد.  
4. **معرفة أساسية بـ HTML/CSS** – مفيدة لكنها ليست إلزامية.

## استيراد الحزم
لبدء العمل، استورد الفئات الأساسية في Java. الاستيراد الصريح الوحيد الذي تحتاجه لهذا المثال هو `java.io.IOException`؛ ففئات Aspose يتم الإشارة إليها بأسماءها المؤهلة بالكامل لاحقًا.

```java
import java.io.IOException;
```

## الخطوة 1: إنشاء مستند HTML بسيط
أولاً، سنكتب ملف HTML بسيط (`document.html`) سيعمل كمصدر لتحويل PDF.

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **نصيحة احترافية:** احفظ ملف HTML في نفس الدليل مع ملف مصدر Java لتجنب مشاكل المسارات.

## الخطوة 2: إعداد تكوين Aspose.HTML
أنشئ كائن `Configuration`. هذا الكائن يعمل كحاوية لجميع الخدمات (بما في ذلك خدمة وكيل المستخدم) التي ستستخدمها لاحقًا.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## الخطوة 3: الوصول إلى خدمة وكيل المستخدم
تتيح لك **User Agent Service** حقن ورقة أنماط مخصصة، وتعيين مجموعة الأحرف الافتراضية، والتحكم في خيارات العرض الأخرى.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## الخطوة 4: تعريف وتطبيق ورقة أنماط المستخدم
الآن نوفر قواعد CSS التي ستُنسق HTML عند عرضه. هنا نستخدم **خدمة وكيل المستخدم** لتعيين ورقة الأنماط.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **لماذا هذا مهم:** من خلال تطبيق ورقة الأنماط على مستوى وكيل المستخدم، تضمن أن الأنماط تُحترم حتى إذا لم يُشر المستند الأصلي إلى ملف CSS.

## الخطوة 5: تحميل مستند HTML مع التكوين المخصص
مرّر كلًا من مسار الملف ومثيل `Configuration` إلى مُنشئ `HTMLDocument`. هذا يربط ورقة أنماط المستخدم بالمستند.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## الخطوة 6: تحويل HTML إلى PDF
مع تنسيق المستند بالكامل، استدعِ الطريقة الساكنة `convertHTML` **لتحويل HTML إلى PDF**. كائن `PdfSaveOptions` يتيح لك ضبط مخرجات الملف بدقة (مثل حجم الصفحة، الضغط).

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **النتيجة:** سيحتوي `user-agent-stylesheet_out.pdf` على العنوان باللون البني والفقرة بخلفية GhostWhite، تمامًا كما تم تعريفه في ورقة الأنماط.

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

## مشكلات شائعة وحلولها
| المشكلة | السبب | الحل |
|-------|-------|-----|
| **إخراج PDF فارغ** | لم يتم تطبيق ورقة الأنماط أو لم يتم تحميل المستند بالتكوين. | تحقق من تمرير `configuration` إلى `HTMLDocument` وأنه تم استدعاء `setUserStyleSheet` قبل التحميل. |
| **تحذير خاصية CSS غير مدعومة** | Aspose.HTML لا يدعم بعض ميزات CSS المتقدمة. | استخدم فقط خصائص CSS المذكورة في وثائق Aspose.HTML أو استخدم أنماط أبسط. |
| **FileNotFoundException** | مسار `document.html` غير صحيح. | استخدم مسارًا مطلقًا أو ضع ملف HTML في جذر المشروع. |

## الأسئلة المتكررة

**س: هل يمكنني تطبيق أنماط مختلفة لعناصر HTML المختلفة؟**  
ج: بالتأكيد! يمكنك تعريف عدد غير محدود من قواعد CSS داخل ورقة أنماط المستخدم.

**س: ماذا لو احتجت لتغيير ورقة الأنماط ديناميكيًا؟**  
ج: استدعِ `setUserStyleSheet` مرة أخرى قبل إنشاء كائن `HTMLDocument` جديد؛ سيتم تطبيق الأنماط الجديدة في التحويل التالي.

**س: هل يمكن استخدام ملفات CSS خارجية مع Aspose.HTML للـ Java؟**  
ج: نعم – يمكنك إما ربط ورقة أنماط خارجية في HTML أو تحميل محتواها وتمريره إلى `setUserStyleSheet`.

**س: كيف يتعامل Aspose.HTML مع خصائص CSS غير المدعومة؟**  
ج: يتم تجاهل الخصائص غير المدعومة، مما يسمح لبقية ورقة الأنماط بالعرض دون أخطاء.

**س: هل يمكنني تحويل HTML إلى صيغ أخرى غير PDF؟**  
ج: نعم، يدعم Aspose.HTML التحويل إلى XPS، TIFF، PNG، JPEG، وغيرها باستخدام فئة `SaveOptions` المناسبة.

## الخلاصة
لقد رأيت الآن كيفية **إنشاء PDF من HTML** عن طريق تعيين ورقة أنماط مخصصة للمستخدم باستخدام Aspose.HTML للـ Java. يمنحك هذا الأسلوب تحكمًا كاملاً في المظهر البصري للملف PDF الناتج، مما يجعله مثاليًا لإنشاء تقارير آلية، فواتير، أو أي سيناريو يتطلب تنسيقًا ثابتًا. لا تتردد في تجربة CSS أكثر تعقيدًا، خطوط خارجية، أو صيغ تحويل إضافية لتوسيع هذا الأساس.

---

**آخر تحديث:** 2025-12-05  
**تم الاختبار مع:** Aspose.HTML للـ Java 24.11 (أحدث نسخة وقت الكتابة)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}