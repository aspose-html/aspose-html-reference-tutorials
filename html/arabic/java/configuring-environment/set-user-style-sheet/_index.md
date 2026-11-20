---
date: 2026-04-05
description: تعلم كيفية إنشاء ملف PDF من HTML عن طريق تعيين ورقة أنماط مخصصة للمستخدم
  في Aspose.HTML for Java، وحول HTML إلى PDF بسهولة باستخدام خدمة وكيل المستخدم.
keywords:
- create pdf from html
- convert html to pdf
- java html to pdf
- generate pdf with css
- configure user agent
linktitle: تعيين ورقة الأنماط للمستخدم في Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: إنشاء PDF من HTML – تعيين ورقة الأنماط الخاصة بالمستخدم في Aspose.HTML للـ
  Java
url: /ar/java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF من HTML – تعيين ورقة الأنماط للمستخدم في Aspose.HTML للـ Java

## المقدمة
في هذا الدرس ستتعلم كيفية **إنشاء PDF من HTML** باستخدام Aspose.HTML للـ Java مع تطبيق ورقة أنماط مخصصة للمستخدم. هل وجدت نفسك ترغب في تعديل مظهر مستندات HTML الخاصة بك بأسلوبك الفريد؟ تخيل أنك تصمم صفحة ويب وتحتاج إلى جعل العناوين بارزة بلون محدد أو الفقرات تبدو متسقة عبر الأجهزة. هنا يأتي دور *ورقة الأنماط للمستخدم* و **User Agent Service**. سنستعرض كل خطوة — من كتابة ملف HTML بسيط، تكوين وكيل المستخدم، وحتى **convert HTML to PDF** — لتتمكن من رؤية النتيجة فورًا.

## إجابات سريعة
- **What does “create PDF from HTML” mean?** يعني أن يتم عرض مستند HTML (مع CSS، الصور، الخطوط، إلخ) وحفظ المخرجات البصرية كملف PDF.  
- **Which Aspose component is required?** مكتبة Aspose.HTML للـ Java توفر محرك التحويل و **User Agent Service**.  
- **Do I need a license for testing?** النسخة التجريبية المجانية تكفي للتطوير؛ تحتاج إلى رخصة تجارية للإنتاج.  
- **Can I use an external CSS file?** نعم – يمكنك ربط أوراق الأنماط الخارجية كما في المتصفح العادي.  
- **How long does the conversion take?** بالنسبة لمستند بسيط مثل الموجود في هذا الدليل، يكتمل التحويل في أقل من ثانية.  
- **Why configure the User Agent Service?** يتيح لك حقن ورقة أنماط مخصصة، ضبط مجموعة الأحرف الافتراضية، والتحكم في خيارات العرض، مما يضمن مخرجات PDF متسقة.  

## ما هو “create PDF from HTML”؟
إنشاء PDF من HTML هو عملية أخذ مستند موجه للويب (HTML + CSS) وعرضه في ملف PDF بتخطيط ثابت. هذا مفيد لإنشاء تقارير، فواتير، أو أي مادة قابلة للطباعة مباشرةً من محتوى الويب.

## لماذا تستخدم خدمة User Agent Service في Aspose.HTML؟
توفر **User Agent Service** لك تحكمًا منخفض المستوى في خيارات العرض مثل مجموعة الأحرف الافتراضية، اللغة، الخطوط،—والأهم لهذا الدرس—ورقة أنماط مخصصة للمستخدم. من خلال تطبيق الأنماط على هذا المستوى، تضمن مخرجات بصرية متسقة حتى إذا كان HTML الأصلي يفتقر إلى CSS الخاص به.

## المتطلبات المسبقة
1. **Aspose.HTML for Java** – قم بتنزيل أحدث ملف JAR من صفحة [Aspose releases page](https://releases.aspose.com/html/java/).  
2. **Java Development Kit (JDK) 8+** – تأكد من أن الأمر `java -version` يُظهر الإصدار 8 أو أعلى.  
3. **IDE** – IntelliJ IDEA أو Eclipse أو NetBeans ستعمل بشكل جيد.  
4. **Basic HTML/CSS knowledge** – مفيد لكنه ليس إلزاميًا.  

## استيراد الحزم
لبدء العمل، استورد الفئات الأساسية في Java. الاستيراد الصريح الوحيد الذي تحتاجه لهذا المثال هو `java.io.IOException`؛ ففئات Aspose سيتم الإشارة إليها بأسماءها المؤهلة بالكامل لاحقًا.

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

> **Pro tip:** احتفظ بملف HTML في نفس الدليل مع مصدر Java لتجنب مشاكل المسارات.

## الخطوة 2: إعداد تكوين Aspose.HTML
أنشئ كائن `Configuration`. هذا الكائن يعمل كحاوية لجميع الخدمات (بما في ذلك **User Agent Service**) التي ستستخدمها لاحقًا.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## الخطوة 3: الوصول إلى خدمة User Agent
تتيح لك **User Agent Service** حقن ورقة أنماط مخصصة، ضبط مجموعة الأحرف الافتراضية، والتحكم في خيارات العرض الأخرى.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## الخطوة 4: تعريف وتطبيق ورقة الأنماط للمستخدم
الآن نوفر قواعد CSS التي ستُنسق HTML عند عرضه. هنا نستخدم **User Agent Service** لتعيين ورقة الأنماط.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **Why this matters:** من خلال تطبيق ورقة الأنماط على مستوى وكيل المستخدم، تضمن احترام الأنماط حتى إذا لم يُشرِ HTML الأصلي إلى ملف CSS.

## الخطوة 5: تحميل مستند HTML مع التكوين المخصص
مرّر كلًا من مسار الملف ومثيل `Configuration` إلى مُنشئ `HTMLDocument`. هذا يربط ورقة الأنماط للمستخدم بالمستند.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## الخطوة 6: تحويل HTML إلى PDF
مع تنسيق المستند بالكامل، استدعِ الطريقة الساكنة `convertHTML` لـ **convert HTML to PDF**. يتيح لك كائن `PdfSaveOptions` ضبط مخرجات الملف بدقة (مثل حجم الصفحة، الضغط).

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **Result:** سيحتوي `user-agent-stylesheet_out.pdf` على العنوان باللون البني والفقرة بخلفية GhostWhite، تمامًا كما تم تعريفه في ورقة الأنماط.

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
| **Blank PDF output** | لم يتم تطبيق ورقة الأنماط أو لم يتم تحميل المستند مع التكوين. | تحقق من أن `configuration` تم تمريره إلى `HTMLDocument` وأنه تم استدعاء `setUserStyleSheet` قبل التحميل. |
| **Unsupported CSS property warning** | Aspose.HTML لا يدعم بعض ميزات CSS المتقدمة. | استخدم فقط خصائص CSS المذكورة في وثائق Aspose.HTML أو استخدم أنماط أبسط. |
| **FileNotFoundException** | مسار غير صحيح إلى `document.html`. | استخدم مسارًا مطلقًا أو ضع ملف HTML في جذر المشروع. |

## الأسئلة المتكررة

**س: هل يمكنني تطبيق أنماط مختلفة لعناصر HTML مختلفة؟**  
**ج:** بالطبع! يمكنك تعريف عدد غير محدود من قواعد CSS حسب الحاجة داخل ورقة الأنماط للمستخدم.

**س: ماذا لو احتجت لتغيير ورقة الأنماط بشكل ديناميكي؟**  
**ج:** استدعِ `setUserStyleSheet` مرة أخرى قبل إنشاء مثيل جديد من `HTMLDocument`؛ سيتم تطبيق الأنماط الجديدة في التحويل التالي.

**س: هل يمكن استخدام ملفات CSS خارجية مع Aspose.HTML للـ Java؟**  
**ج:** نعم، يمكنك إما ربط ورقة أنماط خارجية في HTML أو تحميل محتواها وتمريره إلى `setUserStyleSheet`.

**س: كيف يتعامل Aspose.HTML مع خصائص CSS غير المدعومة؟**  
**ج:** يتم تجاهل الخصائص غير المدعومة، مما يسمح لبقية ورقة الأنماط بالعرض دون أخطاء.

**س: هل يمكنني تحويل HTML إلى صيغ أخرى غير PDF؟**  
**ج:** نعم، يدعم Aspose.HTML التحويل إلى XPS، TIFF، PNG، JPEG، والمزيد باستخدام فئة `SaveOptions` المناسبة.

---

**Last Updated:** 2026-04-05  
**Tested With:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}